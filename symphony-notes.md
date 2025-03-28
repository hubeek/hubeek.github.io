# Symphony notes

_Status: Published_
_Created: 2016-06-07 04:54:56_
_Tags: symfony_

// get version 3.0 name it symfresttest

php composer.phar create-project symfony/framework-standard-edition symfresttest 3.0

// add in composer.json
// require
"symfony/console": "2.4.*@dev"
//
php composer.phar install
//
php bin/console




// Workinghours
php composer.phar create-project symfony/framework-standard-edition workhours 2.3.3

php app/console doctrine:database:create
php app/console generate:bundle
php app/console doctrine:generate:entity
php app/console doctrine:schema:update --force
php app/console generate:doctrine:crud


// udemy course
// composer
curl -sS https://getcomposer.org/installer | php
// symfony
php composer.phar create-project symfony/framework-standard-edition 3.0
//

in composer.json
onder extra

"symfony-assets-install": "symlink",

php composer.phar update -d symfonyCourse/

in controller



use Symfony\Bundle\FrameworkBundle\Controller\Controller;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Route;
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Template;
use Symfony\Component\HttpFoundation\Response;

class DefaultController extends Controller
{
    /**
     * @Route("/hello/{name}")
     * @Template()
     */
    public function indexAction($name)
    {
        $response = new Response(json_encode(array("name"=>"hjh!")));
        $response->headers->set('Content-Type', 'Application/json');
        return $response;
        
    }
}



php bin/console doctrine:generate:entity

php bin/console doctrine:schema:update --dump-sql


php bin/console doctrine:database:create


$em = $this->getDoctrine()->getManager();
        $em->persist($workout);
        $em->flush();
        
        $response = new Response(json_encode(array("addWorkout"=>"","errors"=>0)));
        $response->headers->set('Content-Type', 'Application/json');
        return $response;
        
        
        public function indexAction()
    {
        $workouts = $this->getDoctrine()
        ->getRepository('AppallWorkoutBundle:Workout')
                ->findAll();
        $serializer = new Serializer(array(new GetSetMethodNormalizer()), array('json' => new 
JsonEncoder()));
        $workouts_json = $serializer->serialize($workouts, 'json');
        $response = new Response(json_encode(array("workouts"=>$workouts_json,"errors"=>0)));
        $response->headers->set('Content-Type', 'Application/json');
        return $response;
        
    }


php bin/console doctrine:schema:update --force