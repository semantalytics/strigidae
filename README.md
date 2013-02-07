OWL API profile checker
=======================

(c) 2012-2013 University of Manchester

License: Apache License 2.0 (see LICENSE.TXT)

Author: Stian Soiland-Reyes <soiland-reyes@cs.manchester.ac.uk>



Building
--------

    mvn clean package
    chmod 755 target/profilechecker-0.2-SNAPSHOT.jar
    # This only works on Linux 
    sudo cp target/profilechecker-0.2-SNAPSHOT.jar /usr/local/bin/profilechecker


Usage
-----

Help:

    $ # profilechecker -h 
    $ java -jar target/profilechecker-0.2-SNAPSHOT.jar -h
    Usage: profilechecker.jar <ontology.owl> [profile]

    Available profiles:
    OWL2DLProfile (OWL 2 DL)
    OWL2ELProfile (OWL 2 EL)
    OWL2Profile (OWL 2) -default-
    OWL2QLProfile (OWL 2 QL)
    OWL2RLProfile (OWL 2 RL)
    --all


The <ontology.owl> parameter can be given as a local file name or an
absolute IRI.




With only ontology IRI or file name, will check against default profile
(OWL 2 Full):

    $ java -jar target/profilechecker-0.2-SNAPSHOT.jar http://www.co-ode.org/ontologies/pizza/2007/02/12/pizza.owl

Exit code is 0 if the ontology conforms to OWL 2 Full.    


Checking against a specific profile:    

    $ java -jar target/profilechecker-0.2-SNAPSHOT.jar http://www.co-ode.org/ontologies/pizza/2007/02/12/pizza.owl OWL2QLProfile

    Use of non-superclass expression in position that requires a
      superclass expression:
      ObjectAllValuesFrom(<http://www.co-ode.org/ontologies/pizza/pizza.owl#hasTopping>
      ObjectUnionOf(<http://www.co-ode.org/ontologies/pizza/pizza.owl#MozzarellaTopping>
      <http://www.co-ode.org/ontologies/pizza/pizza.owl#TomatoTopping>))
      [SubClassOf(<http://www.co-ode.org/ontologies/pizza/pizza.owl#Margherita>
      ObjectAllValuesFrom(<http://www.co-ode.org/ontologies/pizza/pizza.owl#hasTopping>
      ObjectUnionOf(<http://www.co-ode.org/ontologies/pizza/pizza.owl#MozzarellaTopping>
      <http://www.co-ode.org/ontologies/pizza/pizza.owl#TomatoTopping>)))
      in <http://www.co-ode.org/ontologies/pizza/pizza.owl>] 
    (..)


Exit code is 0 if the ontology conforms to the specified profile.


Checking against all profiles:


    $ java -jar target/profilechecker-0.2-SNAPSHOT.jar http://www.co-ode.org/ontologies/pizza/2007/02/12/pizza.owl --all
    OWL2DLProfile: OK
    OWL2ELProfile: 187 violations
    OWL2Profile: OK
    OWL2QLProfile: 52 violations
    OWL2RLProfile: 188 violations

Exit code is 0 if the ontology conforms to all profiles.
