Resume de cours

 Java est un langage de programmation orienté objet, conçu pour être portable, sécurisé et robuste. Développé par Sun Microsystems (maintenant Oracle) dans les années 1990, Java permet aux développeurs d'écrire du code qui peut s'exécuter sur n'importe quelle plateforme équipée de la machine virtuelle Java (JVM), grâce à la compilation en bytecode. Ce langage est utilisé pour créer des applications web, mobiles, et des systèmes embarqués. Sa syntaxe est similaire à celle de C++, mais il élimine les complexités de gestion de la mémoire et des pointeurs. Java est également réputé pour son large écosystème de bibliothèques et de frameworks, ce qui en fait un choix populaire pour le développement d'applications d'entreprise.


 Spring Boot est un framework Java basé sur le projet Spring, conçu pour simplifier le développement d'applications Java en réduisant la complexité de la configuration. Il permet de créer des applications autonomes, prêtes à produire des résultats, avec une configuration minimale. Spring Boot propose des conventions et des configurations par défaut pour les projets Spring, ainsi qu'un serveur web embarqué (comme Tomcat ou Jetty), facilitant ainsi le déploiement et la gestion des applications. Il est largement utilisé pour développer des applications web et des services RESTful en raison de sa simplicité, de sa flexibilité et de son intégration facile avec d'autres technologies de l'écosystème Spring.


 En Spring, les annotations sont des métadonnées ajoutées au code source pour configurer et personnaliser le comportement des composants du framework. Elles simplifient la configuration en remplaçant les fichiers XML traditionnels. Voici quelques-unes des annotations les plus courantes en Spring :

1. **@Component** : Indique qu'une classe est un composant Spring, géré par le conteneur Spring. Elle est la super-annotation des autres stéréotypes comme `@Service`, `@Repository`, et `@Controller`.

2. **@Service** : Spécialisation de `@Component`, utilisée pour marquer une classe comme un service métier.

3. **@Repository** : Spécialisation de `@Component`, utilisée pour marquer une classe comme un composant de persistance, souvent pour accéder à la base de données.

4. **@Controller** : Spécialisation de `@Component`, utilisée dans les applications web pour marquer une classe comme un contrôleur MVC.

5. **@RestController** : Combinaison de `@Controller` et `@ResponseBody`, utilisée pour les contrôleurs RESTful, indiquant que les méthodes retournent directement les données (généralement au format JSON ou XML).

6. **@Autowired** : Utilisée pour l'injection automatique des dépendances. Spring injecte automatiquement le bean requis par le constructeur, le setter ou le champ annoté.

7. **@Qualifier** : Spécifie quel bean utiliser lorsqu'il y a plusieurs candidats pour l'injection, en combinaison avec `@Autowired`.

8. **@Value** : Permet d'injecter des valeurs depuis des propriétés de configuration dans les champs ou les méthodes.

9. **@Configuration** : Indique qu'une classe contient des méthodes de configuration et retourne des beans à gérer par le conteneur Spring.

10. **@Bean** : Utilisée dans une classe annotée avec `@Configuration` pour définir un bean à ajouter au conteneur Spring.

11. **@RequestMapping** : Utilisée pour mapper les requêtes HTTP à des méthodes dans les contrôleurs. Elle peut être personnalisée avec des verbes HTTP comme `@GetMapping`, `@PostMapping`, etc.

12. **@Transactional** : Indique que les méthodes ou les classes doivent être exécutées dans une transaction, en assurant la cohérence des opérations de base de données.

Ces annotations simplifient la configuration et la gestion des composants Spring, rendant le code plus lisible et maintenable. En Spring Framework, les composants principaux sont les modèles (models), les ressources (resources), et les contrôleurs (controllers). Voici une vue d'ensemble de chaque composant, les fichiers typiques associés et leur contenu.

### 1. Modèle (Model)
**Rôle :** Représente les données et la logique métier de l'application. Les modèles sont souvent des classes POJO (Plain Old Java Object) qui sont mappées à des tables de base de données.

**Exemple de fichier :** `User.java`

**Contenu typique :**
```java
package com.example.demo.model;

import java.persistence.Entity;
import java.persistence.GeneratedValue;
import java.persistence.GenerationType;
import java.persistence.Id;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

### 2. Ressource (Resource)
**Rôle :** Peut inclure des fichiers de configuration, des propriétés, et tout autre fichier utilisé par l'application (comme des fichiers HTML, CSS, ou des templates).

**Exemple de fichier :** `application.properties`

**Contenu typique :**
```properties
# Configuration de la base de données
spring.datasource.url=jdbc:mysql://localhost:3306/demo
spring.datasource.username=root
spring.datasource.password=secret

# Configuration du serveur
server.port=8080
```

**Autre exemple :** `index.html` (fichier de template Thymeleaf ou autre moteur de template)

**Contenu typique :**
```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome</title>
</head>
<body>
    <h1>Hello, ${name}!</h1>
</body>
</html>
```

### 3. Contrôleur (Controller)
**Rôle :** Gère les requêtes HTTP, manipule les données via le modèle et renvoie une réponse. Les contrôleurs sont des classes annotées avec `@Controller` ou `@RestController`.

**Exemple de fichier :** `UserController.java`

**Contenu typique :**
```java
package com.example.demo.controller;

import com.example.demo.model.User;
import com.example.demo.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/users")
    public String listUsers(Model model) {
        model.addAttribute("users", userService.findAll());
        return "userList";
    }

    @PostMapping("/users")
    public String addUser(@RequestParam String name, @RequestParam String email) {
        User user = new User();
        user.setName(name);
        user.setEmail(email);
        userService.save(user);
        return "redirect:/users";
    }
}
```

### Résumé des fichiers et de leur rôle :
- **Modèle (Model)** : Contient les classes de données. Fichiers typiques : `User.java`.
- **Ressource (Resource)** : Fichiers de configuration et autres ressources nécessaires. Fichiers typiques : `application.properties`, `index.html`.
- **Contrôleur (Controller)** : Gère la logique de traitement des requêtes HTTP. Fichiers typiques : `UserController.java`.

Ces composants interagissent ensemble pour créer une application Spring fonctionnelle en séparant les responsabilités : gestion des données, configuration et logique de présentation.





   .   ____          _            __ _ _   
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \  
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \ 
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / / 
 =========|_|==============|___/=/_/_/_/  
##### tables de la base de données 

tables
1.User:stock des infos sur les clients
---------------------------------------------
Nom de la colone	Type de donnée	Description|
id|	BIGINT|	|clé primaire
username|	VARCHAR|	pseudo unique du client|
email|	VARCHAR|	Email du client|
password|	VARCHAR|	MDP du client|
create_at|	TIMESTAMPS|	Date de créatiion|
update_at|	TIMESTAMPS|	Date de modification|


2.Products: stock les infos sur les produits

Nom de la colone	Type de donnée	Description
id	BIGINT	clé primaire
name	VARCHAR	pseudo unique du client
description	TEXT	description du produit
password	VARCHAR	MDP du client
create_at	TIMESTAMPS	Date de créatiion
update_at	TIMESTAMPS	Date de modification
3.Orders: stock les infos sur les commandes faotes par les clients

Nom de la colone	Type de donnée	Description
id	BIGINT	clé primaire
user_id	BIGINT	Clé secondaire
total_amount	DECIMAL	Montant total
statut	VARCHAR	statuts (encour ... )
create_at	TIMESTAMPS	Date de créatiion
update_at	TIMESTAMPS	Date de modification
4.Oder Items: stock les infos sur les produits inclus dans chaque commande

Nom de la colone	Type de donnée	Description
id	BIGINT	clé primaire
order_id	BIGINT	Clé secondaire=>oders
product_id	DECIMAL	Clé secondaire=>product
quantity	INT	Qté de produits commandée
price	DECIMAL	prix du produit
create_at	TIMESTAMPS	Date de créatiion
update_at	TIMESTAMPS	Date de modification
Relations
*users->orders: un usser peut faire plusieurs commandes *products->orders_items:une commande peut avoir plusieurs items *product->order_items: un produit peut etre commander plusieurs fois

spring.jpa.hibernate.ddl-auto: Cette propriéte est utilisée pour spécifier la stratégie de génèration de schéma de la BDD lors du démarrage de l'application . Hibernate, l'ORM utilisé par défaut dans Spring Boot , peut automatiquement créer, mettre à jour, valider ou gérer le schéma de la BDd en fonction de cette propriété. voici une explication des différentes valeurs qu'on peut attibuer : 1.none: Désactive la gestion automatique du schéma par hiernate.Aucune modification du schéma de BDD ne sera effectué au démarrage de l'applicatio.

2.validate: Hibernate vérifie que le schéma de la Bdd correspond à la sturcture défine dans les entités JPA . Aucune modification du schéma ne sera effectuée, mais se le schéma est incorreste ou ne correspond pas, une exception est levée

3.update: Hibernate met à jour le schema de la BDD pour qu'il corresponde aux entirés JPA définies. cela inclu lèajout de nouvelles tables , colonees,ou contraintes, mais ne supprime ni ne modifie le tables ou colones existantes.

4.create: Hibernate supprime le schéma existant et crée un nouveau schéma à patir des entirés JPA définies. Cela implique de perdre toutes les données existantes puisque le schéma est recrée à chaque démarrage de l'application

5.create-drop:similaire a create, mais avec la particularité signifie que la BDD est recréée a chaque démarrage est supprimée à chaque arrêt de l'application.

Schéma d'une BDD
Le schéma d'une BDD est une représentation de la structure logique des données, incluant des tables, les colones, les relations entre les tables , et les contraintes. Il définit comment les données sont organisées , interconnectés, et gérées pour assurer leur coohérance et intégrité..



hibernate crée la table dans la base de donnée.

###### relations
* 'user'->orders:un user peut faire plusieurs commandes
* 'orders'->order_items:une commande peut avoir plusoeurs items
* 'produits'->orders_items:un produit peut etre commander plusieurs fois dans la journée.












##### Repository

Unrepository est un composant de votre app li qui gère les opérations de CRUD sur les entités dans un BDD En gros c'est la couche qui nous permet de parler à la BDD sans se soucier des sétails.

##### Annotation  @Rrepository
Elle sert à marquer une classe comme étant un repository, c'est à dire un endroit où vous allez interagir avec la BDD.

##### Est-ce obligatoire
Non !quand on implemente déjà une interface comme JpaRepository, Spring detece automatiquement notre repository.

#### @PathVariable vs @RequestBody vs @RequestParam.

 @PathVariable
 on l'utilise pour extraire une  partie variable dans notre chemin d'url.

  vs @RequestBody :
  on l'utilise quand on reçoit des données via post.

 vs @RequestParam.
 on l'utilise  quand on a des paramètres dans l'url sous la methode
 @Bas
 sefinit un mapping simple pour un objet (par ex: varchar  pour string)

 @Temporal
 pour un attribut de type
 @ translent 
 @lob
 indique que la la colonne correspondante en base de données est un LOB (large object)
@table
permet de definit les infos sur la table representant  cette entité en base de donnée

@column
permet de declarer des infos  relatives à la colonne sur laquelle un attribut doit être mappé .
@GeneratedValue
indique la strategy 




Le code que vous avez fourni semble être une classe Java annotée avec des annotations de Lombok et JPA (Java Persistence API). Voici un exemple complet d'une classe Java qui représenterait un modèle de produit en utilisant ces annotations :

```java
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Data
@Entity
@NoArgsConstructor
@AllArgsConstructor
@Table(name = "products")
public class Product {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    private String description;
    private Double price;
    private String imageUrl;

    // Vous pouvez ajouter d'autres champs et méthodes si nécessaire.
}
```

### Explication des annotations :
- **`@Data`** : Génère automatiquement les getters, setters, `toString()`, `equals()`, et `hashCode()` pour tous les champs de la classe.
- **`@Entity`** : Indique que cette classe est une entité JPA qui sera mappée à une table dans la base de données.
- **`@NoArgsConstructor`** : Génère un constructeur sans arguments.
- **`@AllArgsConstructor`** : Génère un constructeur avec un argument pour chaque champ de la classe.
- **`@Table(name = "products")`** : Spécifie le nom de la table dans la base de données à laquelle cette entité est liée (ici, la table s'appelle "products").
- **`@Id`** : Indique le champ qui sera utilisé comme identifiant unique (clé primaire) dans la table.
- **`@GeneratedValue(strategy = GenerationType.IDENTITY)`** : Indique que l'identifiant sera généré automatiquement par la base de données. 

Ce modèle vous permet de gérer des objets de type `Product` qui seront automatiquement mappés à des enregistrements dans la table "products" de votre base de données.






Les annotations que vous mentionnez sont couramment utilisées en Java, principalement avec JPA (Java Persistence API) pour la gestion des entités dans une base de données. Voici une explication de chaque annotation :

### 1. **`@Basic`**
- **Description** : 
  - L'annotation `@Basic` est utilisée pour spécifier les propriétés des champs ou des méthodes d'accès dans une entité JPA. Par défaut, tous les champs non annotés dans une entité sont considérés comme `@Basic`.
- **Utilisation** :
  - Vous pouvez utiliser `@Basic` pour spécifier des propriétés comme si un champ est `optional` ou non.
- **Exemple** :
  ```java
  @Basic(optional = false)
  private String name;
  ```

### 2. **`@Temporal`**
- **Description** : 
  - L'annotation `@Temporal` est utilisée pour spécifier le type de `java.util.Date` ou `java.util.Calendar` qui est mappé à une colonne de type date, time, ou timestamp dans la base de données.
- **Utilisation** :
  - Vous pouvez spécifier si vous voulez que le champ soit mappé en tant que `DATE`, `TIME`, ou `TIMESTAMP`.
- **Exemple** :
  ```java
  @Temporal(TemporalType.DATE)
  private Date birthDate;
  ```

### 3. **`@Transient`**
- **Description** : 
  - L'annotation `@Transient` est utilisée pour indiquer qu'un champ ne doit pas être persisté dans la base de données. Il est ignoré par le moteur JPA lors de la persistance des données.
- **Utilisation** :
  - Utilisez `@Transient` pour des champs qui sont calculés ou qui ne doivent pas être enregistrés dans la base de données.
- **Exemple** :
  ```java
  @Transient
  private int age;  // Calculé à partir de la date de naissance
  ```

### 4. **`@Lob`**
- **Description** : 
  - L'annotation `@Lob` est utilisée pour indiquer qu'un champ doit être traité comme un "Large Object" (LOB) dans la base de données. Elle peut être utilisée pour des types comme `String`, `byte[]`, etc.
- **Utilisation** :
  - Pour des données volumineuses comme des fichiers ou des textes longs.
- **Exemple** :
  ```java
  @Lob
  private String largeText;
  ```

### 5. **`@GeneratedValue`**
- **Description** : 
  - L'annotation `@GeneratedValue` est utilisée pour spécifier que la valeur d'un identifiant sera automatiquement générée par la base de données ou un générateur de valeurs spécifié.
- **Utilisation** :
  - Vous pouvez spécifier la stratégie de génération (`AUTO`, `IDENTITY`, `SEQUENCE`, `TABLE`).
- **Exemple** :
  ```java
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  ```

### Exemple combiné
Voici un exemple d'une classe qui utilise certaines de ces annotations ensemble :

```java
import javax.persistence.*;

@Entity
public class ExampleEntity {
    
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    
    @Basic(optional = false)
    private String name;
    
    @Temporal(TemporalType.TIMESTAMP)
    private Date createdDate;
    
    @Transient
    private int age;  // Non persisté, peut être calculé

    @Lob
    private String description;
    
    // Getters and Setters
}
```

Ces annotations aident à définir comment les champs d'une classe Java doivent être gérés en termes de persistance dans une base de données.


En Java avec Spring Data JPA, il existe plusieurs types de relations qui peuvent être définies entre les entités pour modéliser les relations entre les tables dans une base de données. Voici les principales relations :

### 1. **One-to-One (`@OneToOne`)**
   - **Description** : Une relation un-à-un signifie qu'une entité est liée à une autre entité de manière unique. Par exemple, une personne peut avoir une seule adresse.
   - **Exemple** :
     ```java
     @Entity
     public class Person {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @OneToOne
         @JoinColumn(name = "address_id")
         private Address address;
     }
     
     @Entity
     public class Address {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @OneToOne(mappedBy = "address")
         private Person person;
     }
     ```

### 2. **One-to-Many (`@OneToMany`)**
   - **Description** : Une relation un-à-plusieurs signifie qu'une entité peut être liée à plusieurs autres entités. Par exemple, une catégorie peut avoir plusieurs produits.
   - **Exemple** :
     ```java
     @Entity
     public class Category {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @OneToMany(mappedBy = "category")
         private List<Product> products;
     }
     
     @Entity
     public class Product {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @ManyToOne
         @JoinColumn(name = "category_id")
         private Category category;
     }
     ```

### 3. **Many-to-One (`@ManyToOne`)**
   - **Description** : Une relation plusieurs-à-un signifie que plusieurs entités peuvent être liées à une autre entité unique. Par exemple, plusieurs produits peuvent appartenir à une seule catégorie.
   - **Exemple** :
     ```java
     @Entity
     public class Product {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @ManyToOne
         @JoinColumn(name = "category_id")
         private Category category;
     }
     ```

### 4. **Many-to-Many (`@ManyToMany`)**
   - **Description** : Une relation plusieurs-à-plusieurs signifie qu'une entité peut être liée à plusieurs autres entités, et vice versa. Par exemple, un étudiant peut être inscrit à plusieurs cours, et un cours peut avoir plusieurs étudiants.
   - **Exemple** :
     ```java
     @Entity
     public class Student {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @ManyToMany
         @JoinTable(
             name = "student_course",
             joinColumns = @JoinColumn(name = "student_id"),
             inverseJoinColumns = @JoinColumn(name = "course_id"))
         private List<Course> courses;
     }
     
     @Entity
     public class Course {
         @Id
         @GeneratedValue(strategy = GenerationType.IDENTITY)
         private Long id;
         
         @ManyToMany(mappedBy = "courses")
         private List<Student> students;
     }
     ```

### 5. **Cascade Operations**
   - **Description** : Vous pouvez spécifier des opérations en cascade sur une relation pour qu'elles se propagent automatiquement d'une entité à l'autre. Par exemple, si vous supprimez une catégorie, vous pouvez vouloir supprimer automatiquement tous les produits associés à cette catégorie.
   - **Exemple** :
     ```java
     @OneToMany(cascade = CascadeType.ALL, mappedBy = "category")
     private List<Product> products;
     ```

### 6. **Fetch Types**
   - **Description** : Le type de fetch (`FetchType.LAZY` ou `FetchType.EAGER`) détermine si les données associées à une relation sont chargées immédiatement (`EAGER`) ou seulement quand elles sont explicitement demandées (`LAZY`).
   - **Exemple** :
     ```java
     @OneToMany(fetch = FetchType.LAZY, mappedBy = "category")
     private List<Product> products;
     ```

Ces relations vous permettent de modéliser des interactions complexes entre différentes entités dans votre application Spring. Elles sont fondamentales pour créer des structures de données relationnelles efficaces et maintenables dans vos applications Java basées sur Spring Data JPA.

















