# Export all articles from drupal site to md

_Status: Published_
_Created: 2025-03-28 03:13:09_
_Tags: cli, php, drupal_

```php
<?php

// Bootstrap Drupal
define('DRUPAL_ROOT', getcwd());
require_once DRUPAL_ROOT . '/includes/bootstrap.inc';
drupal_bootstrap(DRUPAL_BOOTSTRAP_FULL);

// Load all article nodes (including unpublished)
$query = new EntityFieldQuery();
$result = $query->entityCondition('entity_type', 'node')
    ->entityCondition('bundle', 'article')
    ->execute();

if (empty($result['node'])) {
    echo "No articles found.\n";
    exit;
}

$nodes = node_load_multiple(array_keys($result['node']));

// Create output folder
$output_dir = 'exported_articles';
if (!file_exists($output_dir)) {
    mkdir($output_dir, 0777, true);
}

foreach ($nodes as $node) {
    $title = $node->title;
    $created = format_date($node->created, 'custom', 'Y-m-d H:i:s');
    $status = $node->status ? 'Published' : 'Unpublished';

    // Get body field (handles language properly)
    $body_items = field_get_items('node', $node, 'body');
    $body = ($body_items && isset($body_items[0]['value'])) ? $body_items[0]['value'] : '';

    // Get tags (taxonomy term names)
    $tags = [];
    if (!empty($node->field_tags)) {
        $langcode = key($node->field_tags);
        foreach ($node->field_tags[$langcode] as $term_ref) {
            $term = taxonomy_term_load($term_ref['tid']);
            if ($term) {
                $tags[] = $term->name;
            }
        }
    }
    $tag_line = !empty($tags) ? "_Tags: " . implode(', ', $tags) . "_\n" : '';

    // Sanitize file name
    $safe_title = preg_replace('/[^a-z0-9]+/i', '-', strtolower($title));
    $safe_title = trim($safe_title, '-');
    $filename = $output_dir . '/' . $safe_title . '.md';

    // Create Markdown content
    $md_content = "# {$title}\n\n";
    $md_content .= "_Status: {$status}_\n";
    $md_content .= "_Created: {$created}_\n";
    $md_content .= $tag_line . "\n";
    $md_content .= $body;

    file_put_contents($filename, $md_content);
    echo "Exported: $filename\n";
}

echo "\n✅ All articles exported to: $output_dir/\n";
```
call it export.php put it the drupal root and run
`php export.php`
tar it and download the file to your liking.