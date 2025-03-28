# Extension for structure your code

_Status: Published_
_Created: 2015-07-26 08:20:00_
_Tags: swift_

<code>
class TestViewController: UIViewController {

  @IBOutlet weak var tableView: UITableView!
  
  override func viewDidLoad() {
    super.viewDidLoad()

    styleNavigationBar()
    }
}

private typealias TableViewDataSource = TestViewController
extension TableViewDataSource: UITableViewDataSource
{
  func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return 0
  }
  
  func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCellWithIdentifier("identifier", forIndexPath: indexPath) as! UITableViewCell
    return cell
  }
}

private typealias TableViewDelegate = TestViewController
extension TableViewDelegate: UITableViewDelegate
{
  func tableView(tableView: UITableView, heightForRowAtIndexPath indexPath: NSIndexPath) -> CGFloat {
    return 64.0
  }
}

private typealias ViewStylingHelper = TestViewController
private extension ViewStylingHelper
{
  func styleNavigationBar()
  {
    
  }
}
</code>