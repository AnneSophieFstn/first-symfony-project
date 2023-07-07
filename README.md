# CP5_Vendredi07/07/23!

1. Créer un controller

    `symfony console make:controller`

2. Lancer le server 
    
    `symfony serve`

3. Fichier template
    `render() `

4. Authentification 
`symfony console make:registration`

5. Connexion a la BDD
`Fichier .env & ligne 27`

6. Create database
`symfony console doctrine:database:create`

7. Migration database
`symfony console make:migration`
`symfony console doctrine:migration:migrate`

8. Create Entity
`symfony console make:entity NameEntity`

A SAVOIR : Si on souhaite ajouter un autre champ on refait la meme manip.

 9. Create CRUD
`symfony console make:crud NameEntity` 

 - Inside files config/packages/security.yaml
 - Si on veut gérer l'accès à certaines routes. 
`L.35 - { path: ^/name-route, roles: ROLE_USER }`

 - Dans ReservationController, on doit preciser qu'une fois l'ordinateur est reserve on change la valeur "taken" par "true".

 - On rajoute `EntityManagerInterface  $em` dans la ligne 27.
 - Dans la boucle **If** 

>$ordinateur = $reservation->getOrdinateur();
$ordinateur->setTaken(true); 
//Gerer les entités a chaque fois qui a une modif on doit executer la fonction persist    
$ em -> persist($ordinateur); 
$em-flush();`

- Afficher les ordinateurs qui sont UNIQUEMENT disponible
- Dans **Form**
- ReservationType
- Dans le builder on met ce code
>$builder
            ->add('ordinateur', EntityType::class,[
                'class' => Ordinateur::class, 
                'query_builder' => function(EntityRepository $er){
                    return $er->createQueryBuilder("o") //allias
                    ->where("o.taken = false");
                }
            ])
            ->add('etudiant')
        ;

15. API
> composer require Api

16. Autres package
- DoctrineExtension
- A voir --> les Traits