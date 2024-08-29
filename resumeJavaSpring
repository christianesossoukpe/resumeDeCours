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


1-table users :infos sur le susers
-------------------------------------------------------------
|nom de la colonne | Type de donnée|Description    |
------------------------------------------------------------|
|id               |BIGINT          |CLE PRIMAIRE            |
|username         |varchar         |pseudo unique du client |           
|email            |varchar         |email du client         |    
|password         |varchar         |MDP du client           |           
|created_at       |Timestampvarchar|date de creation        |    
|updated_at       |Timestampvarchar|date de modification    | 
------------------------------------------------------------|  

2-table products: infos sur kes produits

-------------------------------------------------------------
|nom de la colonne | Type de donnée|Description    |
------------------------------------------------------------|
|id               |BIGINT          |CLE PRIMAIRE            |
|username         |varchar         |pseudo unique du client |           
|email            |varchar         |email du client         |    
|password         |varchar         |MDP du client           |           
|created_at       |Timestampvarchar|date de creation        |    
|updated_at       |Timestampvarchar|date de modification    | 
------------------------------------------------------------| 
3-tables orders: infos sur les commandes
-------------------------------------------------------------
|nom de la  colonne | Type de donnée|Description    |
------------------------------------------------------------|
|id               |BIGINT   |CLE PRIMAIRE                   |
|user_id          |BIGINT     |clé secondaire               |           
|total_amount     |DECIMAL       |montant total             |    
|status           |varchar        |Status(en cours...)      |           
|created_at       |Timestampvarchar|date de creation        |    
|updated_at       |Timestampvarchar|date de modification    | 
------------------------------------------------------------|       

####
4-table orders items: infos sur les produits inclus dans chaque commande.
-------------------------------------------------------------
|nom de la colonne | Type de donnée|Description    |
------------------------------------------------------------|
|id               |BIGINT          |CLE PRIMAIRE            |
|order_id         |BIGINT          |clé secondaire->'orders'|           
|product_id       |BIGINT          |clé secondaire->products|    
|quantity         |INT       |quantité de produits commandée|           
|price            |DECIMAL         |prix du produit         |           
|created_at       |Timestampvarchar|date de creation        |    
|updated_at       |Timestampvarchar|date de modification    | 
------------------------------------------------------------|       

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

















