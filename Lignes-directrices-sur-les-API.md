# Création de services numériques connectés : Lignes directrices sur les API

## Préface

### À propos de ce guide
Ce guide s'adresse à toute personne qui développe des services numériques pour un service public, qu'il fasse partie de la Fonction publique de l'Ontario, d'un organisme gouvernemental ou d'autre chose.

Les présentes lignes directrices se veulent être une feuille de route, et non un barrage. Elles visent à simplifier le développement de services numériques afin que les développeurs et les utilisateurs finaux puissent profiter d'un produit plus uniforme et plus robuste.

## Ce que les API peuvent faire
Les interfaces de protocole d'application (API) laissent les applications se parler de façons structurées. Les développeurs de logiciels créent des API afin de partager des fonctionnalités ou des données provenant d'une application qu'ils ont développée avec toute personne qui souhaite travailler avec elle.

Par exemple, lorsque vous regardez l'appli de météo sur votre téléphone, les renseignements que vous voyez proviennent d'une API fournie par votre service météorologique local. Son API prend les données sur les prédictions météorologiques et les convertit dans un format que d'autres développeurs d'applis peuvent utiliser. Cela permet aux développeurs de se concentrer sur la création d'une interface conviviale (par exemple, l'appli de météo de votre téléphone), sans devoir s'inquiéter de la science sous-jacente aux données.

Les API ne se limitent pas à partager des données : elles peuvent être le tissu conjonctif entre de multiples systèmes associés, mais indépendants. Un organisme, comme le ministère des Transports de l'Ontario, qui délivre les permis de conduire pourrait créer une API qui prend un numéro de permis et vérifie s'il est expiré. Cette API serait très utile pour une entreprise de location de voitures qui souhaitent vérifier si le client possède un permis de conduire valide.

## Pourquoi les API sont importantes pour vous
Les API vous permettent de créer des composants réutilisables et de développer une plateforme, ce qui vous évite d'avoir à réinventer la roue à chaque fois. Essentiellement, elles sont les éléments constitutifs d'un écosystème numérique. Comprendre la valeur des API vous aidera à adopter une approche qui commence par le numérique.

Le partage des données et des processus par l'entremise d'API :

* réduit le travail en double
* encourage la communication et l'apprentissage entre les équipes
* rend plus efficace le développement futur d'applications

En suivant ce guide, vous vous assurerez que vos services sont :

* interopérables avec d'autres plateformes et services
* moins susceptibles d'être limités à un fournisseur ou une technologie en particulier
* sont davantage pérennisés et plus faciles à mettre à jour et à tester

Pour les équipes dans la Fonction publique de l'Ontario, les API permettent également aux organismes de satisfaire plus facilement à la [Directive sur les données ouvertes](https://www.ontario.ca/fr/page/directive-sur-les-donnees-ouvertes-de-lontario), qui exige que toutes les données du gouvernement soient publiques, sauf si elles sont spécifiquement exemptées.

### À qui s'adresse ce guide
Vous devriez lire les présentes lignes directrices si vous êtes :

* **un développeur ou une développeuse de logiciels** ou **un(e) architecte de systèmes** qui recherche des conseils techniques
* **un(e) chef de produit** sur un produit d'API qui doit comprendre le contexte
* **un(e) analyste de gestion** qui se demande si une API est une bonne solution pour votre problème
* **un conseiller ou une conseillère en politiques** pour un service numérique qui cherche à mieux comprendre la manière dont les API peuvent contribuer à réaliser les objectifs en matière de politiques
* **un concepteur ou une conceptrice de contenu**, **un concepteur ou une conceptrice d'expériences**, ou **un(e) praticien(ne) de toute autre discipline pertinente** qui souhaite se familiariser avec les principes décrits dans les présentes, afin de pouvoir y ajouter sa perspective

### Portés par des épaules de géants
Nous avons adapté les présentes lignes directrices pour la Fonction publique de l'Ontario en nous basant sur l'excellent travail d'autres gouvernements numériques, y compris :

* [Le gouvernement du Canada](https://www.canada.ca/fr/gouvernement/systeme/gouvernement-numerique/technologiques-modernes-nouveaux/normes-gouvernement-canada-api.html)
* [Le Service numérique du Royaume-Uni](https://www.gov.uk/guidance/gds-api-technical-and-data-standards) (en anglais)
* [18F (la General Services Administration des États-Unis)](https://github.com/18F/api-standards) (en anglais)
* [Le gouvernement de Nouvelle-Zélande](https://snapshot.ict.govt.nz/guidance-and-resources/standards-compliance/api-standard-and-guidelines/index.html) (en anglais)
* [Le gouvernement de l'État de Victoria, Australie](https://github.com/VictorianGovernment/api-design-standards) (en anglais)

## Facteurs relatifs aux activités et aux processus
Si vous développez une API pour la Fonction publique de l'Ontario, vous devez respecter la [Norme des services numériques](https://www.ontario.ca/fr/page/norme-des-services-numeriques) (NSN) du gouvernement de l'Ontario. Même si vous ne faites pas partie de la FPO, nous vous encourageons tout de même à vous familiariser avec la NSN, qui présente 14 principes clés pour le développement de bons services axés sur les utilisateurs.

### Consommez ce que vous créez
La meilleure façon de vous assurer que votre API est bien conçue consiste à l'utiliser vous-même dans une application en production. Dans le secteur technique, ce processus est appelé « dogfooding ».

Essayez toujours de créer vos API en parallèle avec un cas d'utilisation interne qui sera intégré avec l'API avant que celui-ci soit publié pour un usage externe. Le cas d'utilisation interne peut servir de projet pilote peu visible que vous utilisez pour valider vos hypothèses concernant la manière de concevoir l'API et vous permettra de pivoter et d'adapter votre conception, au besoin. Il vous force également à réfléchir du point de vue de l'utilisateur et de ses besoins.

Assurez-vous que la conception de votre API tient compte des différentes façons dont elle pourrait être utilisée par votre public, y compris :

* les systèmes internes de la FPO
* des partenaires de confiance
* le public

Si vous devez limiter l'accès d'un public à certains composants, intégrez des capacités de gestion des utilisateurs, au lieu de créer de multiples API. Cette approche permettra également de faire ressortir tout problème de sécurité potentiel dès le début, alors qu'ils peuvent être réglés de façon proactive.

### Parlez à vos utilisateurs ([NSN no 1](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-1))
Travaillez avec les personnes qui utiliseront l'API pour s'assurer que votre architecture et votre conception répondent à leurs besoins. Utilisez les services d'experts en conception de l'expérience utilisateur pour effectuer des recherches auprès :

* d'utilisateurs techniques
* de domaines d'affaires et de programmes

Les API devraient être créées pour satisfaire des exigences d'affaires précises afin de résoudre des problèmes concrets. Si vous ne savez pas quel besoin des utilisateurs est satisfait par l'API, ou si vous créez simplement l'API pour exposer des données sans savoir à quoi elles serviront, cela indique probablement que l'API n'est pas la bonne solution.

### Utilisez des normes ouvertes ([NSN no 9](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-9))
Si possible, créez votre API en utilisant des outils, des cadres et des normes ouverts. Les communautés ouvertes qui développent ces outils travaillent grâce à la collaboration et au développement de consensus, et les participants vont de contributeurs individuels qui travaillent dans leurs temps libres à d'importantes entreprises technologiques. La diversité des voix permet de s'assurer que les outils visent l'interopérabilité, la sécurité, la fiabilité et l'accessibilité. De plus, parce que ces outils ne sont pas associés à un fournisseur ou un système en particulier, vous n'exclurez pas les utilisateurs de l'extérieur de la FPO.

### Effectuez de fréquentes itérations ([NSN no 8](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-8))
La Norme des services numériques de l'Ontario inclut [une approche agile du développement](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-8). Cela signifie que vous pouvez bâtir votre application en « itérations » qui améliorent un ensemble de fonctions à la fois, ce qui vous permet :

* de tester rapidement votre service auprès de vrais utilisateurs
* de prouver ou de réfuter vos hypothèses
* de réagir plus rapidement aux changements des exigences, des politiques ou de la technologie

Plus il est facile d'effectuer des itérations avec votre API, plus elle sera facile à utiliser par les autres utilisateurs.

### Intégrez la protection de la vie privée au niveau de la conception ([NSN no 10](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-10))
Bien qu'il soit important de minimiser les obstacles à l'accès aux programmes gouvernementaux, il est également important de protéger les données sensibles et de minimiser le potentiel d'atteintes à la protection des données.

Évaluez les données qui seront partagées par l'entremise de l'API. Lorsque vous travaillez avec :

* des données qui ne sont pas sensibles, créez des API qui peuvent être utilisées par le public, avec un minimum d'obstacles
* des données sensibles, mettez en place des mesures appropriées en matière juridique, de sécurité et de protection de la vie privée pour éviter tout mésusage des données

Pour obtenir de plus amples renseignements, consultez les [sept principes de la protection de la vie privée au niveau de la conception](https://www.ryerson.ca/pbdce/certification/seven-foundational-principles-of-privacy-by-design/) (en anglais).

### Faites connaître vos intentions ([NSN no 5](https://www.ontario.ca/fr/page/norme-des-services-numeriques#section-5))
Tenez vos utilisateurs au courant de vos plans pour l'API. Travaillez avec eux pour les aider à comprendre les répercussions de tout changement majeur prévu.

Lorsque vous publiez des mises à jour à une API qui contiennent des changements qui ne sont pas [rétrocompatibles](#utilisez-la-gestion-semantique-de-version) et qui exigent que vos partenaires développeurs mettent leur code à jour, assurez-vous de définir et de communiquer des échéanciers clairs de dépréciation. Cela permet aux développeurs de passer à la nouvelle version avant que l'ancienne version qu'ils utilisent soit mise hors service, et évite de perturber leur travail.

Assurez-vous que chaque API a au moins un point de contact désigné pour les équipes qui l'utilisent :

* toutes les API ont besoin d'un compte de courriel publié pour le soutien
* un numéro de téléphone est également requis pour les API très critiques
* l'idéal est de publier une page de statut sur laquelle les utilisateurs peuvent trouver les indisponibilités prévues et imprévues, et les derniers renseignements concernant la disponibilité et le statut de l'API

### Assurez-vous que vous avez vraiment besoin d'une API
Les API comptent parmi les nombreuses façons d'intégrer les données et les fonctions entre les systèmes, mais elles ne sont pas toujours la meilleure ou l'unique solution. Si vous devez archiver une grande quantité de relations complexes entre les données une fois par an, un [système de transfert de données en vrac](https://fr.wikipedia.org/wiki/Transmission_de_donn%C3%A9es) pourrait s'avérer préférable. Ou s'il est peu probable que l'application client et le serveur soient en ligne en même temps et ils doivent communiquer de façon asynchrone, une [file de messagerie](https://aws.amazon.com/fr/message-queue/) pourrait être une solution plus appropriée. Les API sont à leur plus utile si vous soutenez des interactions entre les systèmes et l'accès aux données en temps réel.

## Facteurs techniques
### Concevez des API passives
Chaque appel à l'API doit contenir tous les renseignements requis pour répondre à la demande, sans s'attendre à ce que le serveur se souvienne de quoi que ce soit concernant des demandes ou des contextes précédents. Cela porte le nom de conception passive.

Ne stockez pas de renseignements concernant les états des sessions sur le serveur de l'API. Toute forme de gestion des états—par exemple sous la forme de témoins ou d'ID de session—doit être conservée par le client qui envoie la demande. Il est donc plus facile pour votre API de détecter les erreurs et de les réparer, car chaque erreur est contenue à l'intérieur d'une seule demande et ne concerne pas la totalité de l'état du serveur.

La conception d'une API passive améliore également l'évolutivité de votre serveur, car les ressources de traitement peuvent être libérées rapidement pour chaque demande, sans qu'il soit nécessaire de conserver les transactions incomplètes en mémoire cache.

### Si possible, respectez le style REST
Dans la grande majorité des cas d'utilisation, nous recommandons la conception d'API [REST](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) (en anglais). Le transfert d'état représentationnel (REST) est la plus importante norme d'intégration avec les services dans le nuage, et est également la norme définie par la majorité des autres gouvernements qui ont des programmes d'API bien établis. Suivez les [meilleures pratiques](https://restfulapi.net/) (en anglais) du secteur lorsque vous effectuez la conception et le développement de votre API REST. Notamment :

#### Représentez les ressources en tant qu'URL
Chaque URL terminale dans la conception d'une API REST devrait représenter une entité, une ressource ou un objet de gestion. Par exemple, une API de ServiceOntario (SO) pourrait fournir des points terminaux permettant de voir des renseignements concernant un seul emplacement de SO.

* **À FAIRE** : `api.ontario.ca/bureaux/emplacement/college-park`

N'utilisez pas les points terminaux pour effectuer des opérations sur ces entités ou objets. Cela signifie que vos schémas d'URL devraient être composés de noms et pas de verbes.

* **À NE PAS FAIRE** : `api.ontario.ca/obtenirHeuresdOuverture/college-park`

#### Utilisez des URI pour identifier les ressources
Si les données de la réponse contiennent des références à d'autres ressources dans l'API, incluez une URL complète vers le point terminal pour cette ressource. Cela permettra à l'utilisateur de suivre les références des données pour des activités futures avec un minimum d'efforts.

Si des données sont renvoyées dans une réponse, utilisez des identificateurs de ressources uniformes (URI) pour identifier de façon unique chaque ressource de données. Cela permettra au client ou au système consommateur de faire référence directement à cette donnée pour des activités futures, avec un remaniement mineur.

Par exemple, un point terminal qui fournit des renseignements sur les emplacements de ServiceOntario à proximité d'une adresse donnée devrait être lié directement aux points terminaux pour chacun de ces emplacements, au lieu de se contenter d'énumérer les noms.

* **À FAIRE** :
```
{
  proche: [{
    nom: "University Avenue",
    url: "api.ontario.ca/location/university-ave"
  }]
}
```

* **À NE PAS FAIRE** :
```
{
  proche: ["University Avenue"]
}
```

#### Renvoyez les données en format JSON
Utilisez la notation des objets du langage JavaScript ([JSON](https://www.json.org/) (en anglais)) et d'autres représentations basées sur JSON (comme [JSON-LD](https://json-ld.org/) (en anglais)) pour transmettre des données entre un client et un serveur. Les réponses envoyées par l'API au client devraient être formées comme des objets et non des tableaux or des valeurs. Les tableaux ne sont pas suffisamment robustes pour inclure des métadonnées adéquates concernant l'objet résultat, ce qui peut rendre plus difficile l'itération lors de la conception des données.

Par exemple, un point terminal qui énumère tous les emplacements de ServiceOntario devrait inclure leur nombre.

* **À FAIRE** :
```
{
  totale: 234
  emplacements: [ ... ]
}
```

* **À NE PAS FAIRE** :
```
[
  { id: university-ave ... },
  { id: college-park ... }
]
```
Assurez-vous que la conception de vos objets de données est prévisible et facile à utiliser. Suivez une grammaire cohérente pour nommer les clés d'objets, et n'utilisez pas de données réelles pour créer des clés d'objets dynamiques.

#### Ne surchargez pas les méthodes d'appel au protocole HTTP

Chaque [méthode d'appel au protocole HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) (en anglais)—aussi appelée verbe HTTP—devrait représenter une seule opération sur une ressource donnée ou une liste de ressources. N'utilisez pas de paramètres de demande pour définir des opérations supplémentaires; par exemple, n'utilisez pas GET pour faire quelque chose d'autre que récupérer des données. Voici les utilisations idiomatiques des verbes HTTP dans le contexte d'une API REST :

* `GET` – obtenir une ressource
* `POST` – créer une nouvelle ressource
* `PUT` – mettre à jour ou remplacer une ressource existante
* `DELETE` – supprimer une ressource

Ces opérations sont également parfois appelées « `CRUD` » (Create, Read, Update, Delete – Créer, lire, mettre à jour, supprimer).

#### Utilisez des entêtes d'acceptation standard

Toute négociation entre le client et le serveur concernant le type de données demandées doit être effectuée en utilisant des [entêtes HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) (en anglais). Les entêtes de demande ACCEPT et CONTENT-TYPE sont obligatoires, et les entêtes AUTHORIZATION sont obligatoires pour les API sécurisées. Les clés de l'API doivent être transférées dans l'entête, et non dans l'URL de demande.

Si votre API accepte plusieurs langues, l'entête ACCEPT-LANGUAGE doit être envoyé par le client, et le serveur doit renvoyer le contenu dans la langue demandée. Si l'entête de langue n'est pas défini dans un système multilingue, le contenu doit être renvoyé dans toutes les langues acceptées. Les différentes langues devraient être imbriquées sous les [codes de langue BCP-47](https://tools.ietf.org/html/bcp47) (en anglais) (p. ex., « en », « fr ») comme clés d'objets. Les données renvoyées dans la réponse doivent contenir au minimum l'entête CONTENT-TYPE.

#### Utilisez des codes d'erreur normalisés

Lorsque vous créez des API REST, utilisez des [codes d'état HTTP](https://restfulapi.net/http-status-codes/) (en anglais) standard. Respectez les [anomalies SOAP 1.2](http://www.w3.org/TR/soap12-part1/#soapfault) (en anglais) lorsque vous créez des API SOAP. Évitez de développer des codes d'erreur et des schémas de données sur mesure : le client doit faire davantage de travail pour les analyser.

#### Solutions de rechange à REST

Les API REST ne seront pas la meilleure solution pour chaque problème d'affaires, particulièrement s'il existe des contraintes techniques du côté du fournisseur ou du côté du consommateur. Voici quelques exemples d'autres architectures d'API que vous pourriez considérer :

##### SOAP
[Le protocole SOAP (Simple Object Access Protocol)](https://en.wikipedia.org/wiki/SOAP) (en anglais) est un protocole permettant d'échanger des renseignements structurés sur un réseau, le plus souvent [par langage XML (langage de balisage extensible)](https://en.wikipedia.org/wiki/XML) (en anglais) sur HTTP. Les normes sont plus strictes et sa mise à jour exige plus de temps système que les systèmes REST. Cela pourrait être utile si vous avez des exigences en matière de conformité. Les mises à jour SOAP devraient respecter les [spécifications SOAP 1.2](http://www.w3.org/TR/soap12-part1/) (en anglais) et être conformes à [WS-I Basic Profile 2.0](http://ws-i.org/profiles/BasicProfile-2.0-2010-11-09.html) (en anglais).

D'autres lignes directrices sur l'utilisation de SOAP dans la FPO sont disponibles dans le document [NTI-GO 24.0 Norme omnibus pour les services Web](https://www.ontario.ca/fr/document/nti-go-240-norme-omnibus-pour-les-services-web).

##### GraphQL
[GraphQL](https://en.wikipedia.org/wiki/GraphQL) (en anglais) est un langage d'interrogation pour la création d'API conçues pour fonctionner avec un seul point terminal. GraphQL exige que le consommateur définisse la structure des données qu'il souhaite obtenir auprès du fournisseur, ce qui procure un contrôle plus granulaire sur les formats de données et une analytique plus détaillée. Les mises en œuvre de GraphQL devraient respecter les [meilleures pratiques du secteur](https://graphql.org/learn/best-practices/) (en anglais).

##### RPC
[L'appel de procédure à distance (Remote Procedure Call ou RPC)](https://en.wikipedia.org/wiki/Remote_procedure_call) (en anglais) est un style de conception d'API qui met l'accent sur les opérations (c.-à-d. procédures) plutôt que sur les ressources. Le consommateur accède à des points terminaux qui invoquent directement une fonction donnée sur le serveur du fournisseur. Ce style de conception d'API est préférable si des interactions plus complexes que les opérations CRUD sont requises. Il est souvent utilisé conjointement avec la conception d'API REST, bien que cela ne soit pas strictement nécessaire.

##### gRPC
[gRPC](https://grpc.io/) (en anglais) est un système de RPC ouvert initialement développé par Google. Il utilise un protocole de sérialisation différent de la plupart des API HTTP, ce qui améliore la vitesse de communication des demandes. Il est généralement utilisé de façon interne entre les microservices, car il exige un contrat défini (c.-à-d. un protofichier) entre les services.

### Effectuez la conception de structures de données ayant un sens
La conception des structures de données qui alimentent le programme de fond de l'API peut être tout aussi importante que la conception de l'architecture logicielle de l'API elle-même. Réfléchissez bien à la façon de structurer les données qui sont renvoyées au client par l'API. Des métadonnées et un codage cohérent permettent de s'assurer que les API sont interopérables au sein des organisations et entre celles-ci, et des données de réponse clairement structurées sont plus faciles à manipuler par le client.

#### Utilisez des schémas de données descriptifs
N'utilisez pas de structures de données génériques, comme des pairs clé-valeur ou des champs génériques. Les contraintes d'un objet de donnée quelconque devraient être apparentes à la lecture de la définition du schéma pour ce type d'objet. Consultez [Schema.org](https://schema.org/) (en anglais) pour voir des exemples de schémas de données bien conçus.

#### Utilisez les modèles d'information qui sont des normes dans le secteur pour votre discipline
Si possible, évitez de définir votre propre modèle d'information Examinez plutôt vos besoins d'affaires et voyez quels modèles d'information sont utilisés par d'autres praticiens dans votre secteur—par exemple, vous pourriez utiliser [HL7](https://www.hl7.org/) (en anglais) pour les données sur la santé, ou [GTFS](https://developers.google.com/transit/gtfs/) (en anglais) pour des données de transport en commun. Si vous devez définir votre propre modèle d'information, créez-en un qui ne dépend pas d'une technologie ou d'une plateforme en particulier, et évitez de vous limiter à un fournisseur en particulier.

Si vous êtes un développeur au sein de la Fonction publique de l'Ontario, vous pouvez également consulter les ressources internes suivantes sur l'architecture de l'information :

* [Standards for Developing Architecture](https://intra.ontario.ca/iit/standards-for-developing-architecture) (en anglais)
* [Common Elements Data Model - Party LDM](https://intra.ontario.ca/wordpress/uploads/2017/05/CDEM-Party-LDM-v2.5.pdf) (en anglais)
* [Common Data Elements - Address LDM](https://intra.ontario.ca/wordpress/uploads/2017/08/CDEM-Address-LDM-v2.3.pdf) (en anglais)
* [NTI-GO 56.3 Annexes du Manuel sur la modélisation de l'information](https://www.ontario.ca/fr/document/nti-go-563-annexes-du-manuel-sur-la-modelisation-de-linformation-mmi) (en anglais)

#### Rendez abstraites les structures de vos données brutes
N'exposez pas les données brutes de vos systèmes dorsaux aux utilisateurs finaux. Toutes les données devraient traverser une phase de transformation afin que les détails inutiles soient supprimés et que l'objet de donnée qui en résulte soit conçu pour ce dossier d'analyse. L'exposition des structures des données brutes peut exposer de l'information sur vos activités internes et créer des vulnérabilités en matière de sécurité. Si vous devez exposer des données brutes, faites-le seulement pour des API de données ouvertes, de rapports et de statistiques.

Par exemple, une API transactionnelle qui effectue le suivi de bons de commande pourrait être par-dessus d'une base de données contenant des renseignements confidentiels sur les fournisseurs. Ces renseignements devraient être supprimés avec les autres données inutiles, afin que l'utilisateur ne voie que le numéro de commande et le statut.

#### Omettez les données de débogage
Toutes les données de la réponse devraient avoir un sens pour le client et ne pas exposer de détails techniques dont le développeur pourrait avoir besoin pour le débogage. N'incluez pas les erreurs techniques, le vidage des fils, les identifiants de processus ou les messages d'erreur dans les données de la réponse, même si l'appel à l'API n'a pas réussi. L'exposition de ces renseignements dans un environnement de production peut avoir des répercussions majeures sur la sécurité. Investissez plutôt dans un [système d'enregistrement](#consignez-lactivit%C3%A9-et-la-performance) robuste.

#### Soyez clair concernant le codage de vos données
Utilisez le format [UTF-8](http://unicode.org/faq/utf_bom.html#utf8-1) (Unicode Transformation Format-8) (en anglais) comme type de codage standard pour la totalité du texte et des représentations textuelles des données par l'entremise d'API. Si des contraintes techniques ou d'affaires exigent l'utilisation d'une norme de codage autre que UTF-8, identifiez clairement la norme dans l'entête de réponse charset et la documentation de l'API.

#### Utilisez un format uniforme de date et d'heure
Suivez la norme internationale [ISO 8601](https://www.iso.org/fr/standard/40874.html) en temps universel coordonné ([UTC](https://www.timeanddate.com/time/aboututc.html) (en anglais)) pour les champs standard de date et d'heure dans les données renvoyées par l'API. Le format de date est `<yyyy-mm-dd>`, et le format de l'heure système est `<yyyy-mm-dd>T<hh:mm:ss>Z` en format 24 heures. Cela permet de représenter la date de la même façon dans les deux langues. Toute autre représentation de l'heure dans les données source doit être convertie à ce format par l'API.

### Pensez avant d'itérer
Assurez-vous de minimiser l'impact sur les utilisateurs de votre développement agile et itératif afin qu'ils ne soient pas victimes de perturbations inutiles ou inattendues.

#### Utilisez la gestion sémantique de version
Chaque mise à jour publiée d'une API, si petite soit-elle, doit porter un nouveau numéro de version dans votre système de contrôle des versions. Suivez la [norme de gestion sémantique de version](https://semver.org/lang/fr/) afin d'indiquer clairement la portée de chaque version et si elle est susceptible de contenir des changements non rétrocompatibles. Chaque version devrait porter un identifiant `v<majeure>.<mineure>.<correctif>` (par exemple, `v2.3.1`). Les versions majeures sont les seules qui devraient introduire des changements importants qui pourraient être non rétrocompatibles. Les versions mineures devraient désigner des ajouts de fonctionnalités rétrocompatibles ou des attributs facultatifs, tandis que les correctifs ne devraient être que des corrections de bogues ou des anomalies mineures qui n'affectent pas le changement de l'API.

#### Indiquez la version majeure dans l'URL
La version majeure de votre API devrait être indiquée dans l'URL des API REST, par exemple api.ontario.ca/v3/endpoint. Cela permet de soutenir plus facilement d'anciennes versions d'une API en même temps que la version la plus récente lors de la publication d'un changement majeur qui n'est pas rétrocompatible. Ne transférez pas les versions en tant que paramètres ou entêtes de demandes.

#### Dépréciez de façon gracieuse
Soutenez au moins une version majeure précédente pendant une période de transition pour vous assurer que vos utilisateurs ont un préavis suffisant pour transférer leur travail, et communiquez vos feuilles de route du développement avec vos utilisateurs. Par exemple, dans un système REST, vous pouvez utiliser [l'entête Warning](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) (en anglais) de HTTP pour annoncer les changements prochains.

#### Effectuez constamment des essais
Vous devriez adopter la méthode d'intégration continue et de livraison continue (CI/CD), soutenue par des outils d'automatisation et des essais de sécurité intégrés. Cela crée un filet de sécurité qui permet l'itération rapide et devient la première étape sur un parcours vers [l'automatisation DevOps](https://aws.amazon.com/fr/devops/what-is-devops/) (en anglais). DevOps est une philosophie et une culture organisationnelle qui intègre étroitement le déploiement, les activités et la sécurité avec le développement quotidien pour une efficacité et une qualité maximales.

Assurez-vous que votre suite de tests inclut des tests unitaires, des tests d'intégration et des tests de bout en bout. Ceux-ci devraient mesurer la performance sous une charge moyenne, tout en identifiant les seuils de performance au-delà desquels l'API devient instable. N'effectuez pas vos tests uniquement dans des conditions idéales.

Par exemple, si vous testez de multiples composants qui communiquent ensemble, assurez-vous que vos tests de bout en bout ont lieu dans un environnement réel, afin d'obtenir les renseignements les plus exacts sur la latence. Regardez « [Avoiding Microservice Megadisasters – Jimmy Bogard](https://www.youtube.com/watch?v=gfh-VCTwMw8) (en anglais) » pour voir pourquoi il s'agit d'une pratique louable.

### Intégrez la sécurité au niveau de la conception
Même si votre API n'expose pas de données protégées ou privilégiées, il est tout de même important d'étudier la manière d'incorporer la conception d'une architecture sécurisée dans votre système. Cela est une bonne pratique qui vous permettra également de préparer votre API pour les développements futurs. Les lignes directrices devraient être considérées comme des mesures de sécurité de base. Des mesures de contrôle supplémentaires (par exemple, chiffrement au niveau du message, authentification mutuelle et signatures numériques) pourraient également être requises, selon le niveau de sensibilité des données.

Pour obtenir de plus amples renseignements, consultez les [dix principes de la sécurité au niveau de la conception](https://www.owasp.org/index.php/Security_by_Design_Principles) (en anglais) présentés par l'Open Web Application Security Project.

#### Imposez une communication sécurisée
Il ne faut jamais envoyer ou stocker des données sensibles en clair. Évitez d'utiliser une connexion non sécurisée ou non chiffrée dans la mesure du possible, même avec des données qui ne sont pas sensibles.

* Les données sensibles doivent être envoyées via TLS version 1.2 ou plus, et tous les certificats doivent être SHA-256 avec une longueur de clé minimale de 2048.
* Le trafic non sécurisé envoyé sur HTTP devrait être refusé au lieu d'être réacheminé automatiquement à HTTPS. Suivez les normes de cybersécurité des [normes de technologies de l'information (NTI-GO) du gouvernement de l'Ontario ](https://www.ontario.ca/fr/page/normes-en-technologie-de-linformation#section-6) lorsqu'elles sont pertinentes, ou consultez le [Centre canadien pour la cybersécurité](https://cyber.gc.ca/fr/directives) (en anglais).

#### Ne mettez pas de données sensibles dans les URL de demande
N'acceptez jamais de données sensibles dans les URL ou les chaînes d'interrogation, y compris les clés API. Le client doit envoyer cette information dans un entête HTTP ou les données utiles d'un message JSON afin qu'elle puisse être chiffrée correctement. Même avec le chiffrement pendant le transport, les chaînes URL peuvent être suivies et compromises.

#### Établissez une politique d'accès clairement définie
Authentifiez, autorisez et validez toujours les demandes entrantes. À l'exception des API ouvertes publiques suivantes, toutes les API devraient mettre en œuvre des contrôles sur l'autorisation basés sur des clés. Les API ne doivent permettre l'accès qu'aux clés d'API valides et restreindre l'accès autrement. Vous pourriez devoir envisager d'autres approches de gestion des abus, y compris la limitation du débit par adresse IP.

Désactivez tout verbe HTTP inutilisé et rejetez les demandes invalides vers ces points terminaux. Si cela est pertinent, utilisez des normes du secteur comme [ OpenID Connect](http://openid.net/connect/) (en anglais) et Open Authorization 2.0 ([OAuth 2.0](https://oauth.net/2/) (en anglais)) comme protocole d'authentification pour les API REST. Utilisez le Security Assertion Markup Language 2.0 ([SAML 2.0](http://docs.oasis-open.org/security/saml/Post2.0/sstc-saml-tech-overview-2.0.html) (en anglais)) pour les API SOAP.

#### Mettez en œuvre la gestion des jetons
Nous recommandons fortement une authentification basée sur des jetons. L'idéal est d'utiliser un jeton ouvert qui est standard dans l'industrie.

* [JSON Web Token (JWT)](https://jwt.io/) (en anglais) pour les API REST
* [WS-Security SAML Token Profile](http://docs.oasis-open.org/wss-m/wss/v1.1.1/wss-SAMLTokenProfile-v1.1.1.html) (en anglais) pour les API SOAP

Évitez les schémas de jetons exclusifs à un fournisseur, et ne tentez pas de créer un schéma de jetons sur mesure à partir de zéro. Tous les jetons doivent expirer au bout d'un délai raisonnable, selon les exigences de la sécurité. Par exemple, le jeton utilisé pour la limitation de la vitesse peut avoir un délai d'expiration plus long que les jetons utilisés pour l'authentification. Dans le cas de SAML, l'expiration de l'assertion doit contrôler la validité de toute la session d'authentification et d'autorisation.

### Développez des compétences internes en matière de sécurité concernant des vecteurs potentiels de menaces
Il existe de nombreuses façons d'attaquer et de compromettre une API. Elles portent le nom de vecteurs de menaces. Comme il est impossible de les couvrir tous dans ce guide, il est important que chaque équipe de développement acquière une intuition et des compétences internes relativement aux menaces possibles et effectue la conception de l'API afin de la rendre résiliente pour vos propres besoins.

Voici certaines des attaques les plus courantes sur les API :

* Lors des [attaques par injection](https://cheatsheetseries.owasp.org/cheatsheets/Injection_Prevention_Cheat_Sheet.html#introduction) (en anglais), les attaquants envoient des données entrantes mal formées à l'API dans le but d'exposer les lacunes en matière de sécurité. Certaines des formes les plus connues de cette attaque comprennent l'injection SQL et les demandes XPath à XML. Elles peuvent être partiellement atténuées avec la validation des données entrantes.
* Lors des [attaques par rejeu](https://auth0.com/docs/security/common-threats#replay-attacks) (en anglais), les attaquants copient la demande valide d'un utilisateur et se font passer pour celui-ci. Selon le niveau d'accès dont disposait l'utilisateur, les attaquants pourraient voir et détruire des données privées. Elles peuvent être partiellement atténuées avec de courts délais d'expiration des jetons, l'inscription des jetons utilisés sur une liste noire, et des mots de passe à usage unique.

### Validez les données saisies par les utilisateurs
Toute donnée saisie par un utilisateur devrait être validée dès sa réception, afin que seules des données bien formées et assainies soient traitées par votre API. Cela rendra votre API plus sécuritaire, en plus d'atténuer les erreurs causées par des demandes mal formées.

#### Définissez des paramètres de demande clairs
Définissez l'aspect d'une demande appropriée à votre API, y compris une limite sur la taille des demandes, le type de contenu, et la plage et le format de tout champ spécifique. Si vous acceptez des chaînes de saisie, envisagez de les limiter (par exemple, en utilisant des expressions normales).

#### Limitez les interrogations ouvertes
Non seulement les interrogations dynamiques et ouvertes constituent un vecteur de menace dangereux, mais elles peuvent également consommer une quantité excessive de ressources de traitement. Consacrez des efforts dès le début à identifier tous les cas d'utilisation valides des interrogations, et effectuez la conception de l'API afin d'y répondre spécifiquement. Si vous devez permettre aux utilisateurs d'injecter des chaînes d'interrogation ouvertes ou des objets dans une API, faites-le seulement pour des API de données ouvertes, de rapports et de statistiques. Ne permettez jamais d'interrogations ouvertes vers une API contenant des données maîtresses, ni vers des API transactionnelles ou commerciales. GraphQL peut être utilisé à des fins de statistiques, d'analytique et de rapports, mais il ne devrait pas être utilisé pour soutenir des transactions d'affaires.

#### Faites attention aux caractères de remplacement
Les caractères de remplacement dans les API peuvent être dangereux sur le plan de la performance. Si des caractères de remplacement sont permis, assurez-vous qu'il y a des restrictions sur ceux qui le sont et sur le nombre de paramètres qui peuvent les accepter, afin d'éviter le renvoi d'un volume important de données. Il est préférable de refuser une interrogation contenant trop de caractères de remplacement plutôt que de créer un délai d'inactivité dans votre base de données en arrière-plan.

#### Ne validez pas trop
Avant de valider les données entrantes, assurez-vous que les hypothèses que vous faites concernant vos données d'utilisateur sont universellement vraies. Par exemple :

* les noms ne sont pas toujours « Prénom 2e prénom Nom de famille » : [Mensonges sur les programmeurs croient au sujet des noms](https://www.kalzumeus.com/2010/06/17/falsehoods-programmers-believe-about-names/) (en anglais)
* Les jours ne comptent pas toujours 24 heures : [Mensonges sur les programmeurs croient au sujet de l'heure](https://infiniteundo.com/post/25326999628/falsehoods-programmers-believe-about-time) (en anglais)
* Les adresses de courriel peuvent contenir des caractères étonnants : [Je savais valider une adresse de courriel, jusqu'à ce que je lise le RFC](https://haacked.com/archive/2007/08/21/i-knew-how-to-validate-an-email-address-until-i.aspx/) (en anglais)

### Consignez l'activité et la performance
De bonnes mesures constituent la base de bonnes décisions fondées sur les preuves. Les journaux peuvent fournir des renseignements concernant les tentatives d'attaques, faciliter les analyses rétrospectives, évaluer la performance du système et suggérer des domaines d'amélioration pour le produit ou les fonctions.

#### Définissez les mesures de la performance
Différentes applications mesurent la réussite différemment. Plutôt que d'utiliser les mêmes tests de performance pour chaque API, identifiez vos indicateurs clés de performance avant le lancement, et effectuez la conception d'instruments de mesure qui ciblent spécifiquement ces indicateurs. La latence et le temps de réponse vous fourniront différentes informations sur votre API comparativement à la croissance du nombre d'utilisateurs.

#### Maintenez des journaux qui ont un sens
Tous les accès aux API devraient être consignés en utilisant les normes de journalisation du secteur (par exemple, le [format commun d'événement](https://help.deepsecurity.trendmicro.com/Events-Alerts/syslog-parsing.html) (en anglais)). Si cela est pertinent, suivez les exigences en matière de journalisation dans [NTI-GO 25.0 Exigences générales en matière de sécurité](https://www.ontario.ca/fr/page/nti-go-250-exigences-generales-en-matiere-de-securite) (sections 3.4.2 et 3.4.3) et [NTI-GO 25.13 Exigences en matière de sécurité pour les applications Web](https://www.ontario.ca/fr/page/nti-go-2513-exigences-en-matiere-de-securite-pour-les-applications-web) (section 2.9). Ces journaux devraient être intégrés à un endroit central et doivent inclure, au minimum, les identifiants du système et les identifiants individuels du client qui fait la demande, ainsi que l'heure système. Assurez-vous de ne pas consigner accidentellement des renseignements confidentiels (p. ex., mots de passe).

#### Vérifiez régulièrement les journaux
Les journaux des API devraient être vérifiés régulièrement afin de surveiller l'existence de tendances suspectes en matière d'utilisation ou d'accès, par exemple des demandes après les heures d'ouverture, un volume de demandes inhabituellement élevé ou des échecs répétés de validation des données entrantes. Les événements suspects doivent être envoyés au Centre des opérations en matière de cybersécurité de la Division de la cybersécurité du ministère des Services gouvernementaux et des Services aux consommateurs.

#### Effectuez un audit des accès aux données sensibles
SI votre API fournit des données personnelles ou sensibles, vous devez consigner qui a accédé aux données et à quel moment. Cela est requis pour répondre à des demandes d'accès par l'objet des données, et contribue également à prévenir la fraude ou le mésusage. Consultez votre service juridique pour obtenir les exigences des politiques sur la conservation et de la garde des données.

### Optimisez la performance
Pour que votre API puisse répondre aux besoins de tous les utilisateurs, examinez bien la taille de chaque charge et le taux de réponse. La performance de l'API devrait être évaluée périodiquement afin de vous assurer de toujours satisfaire aux besoins d'affaires existants ou projetés.

#### Surveillez et testez la performance
Il est important que votre API renvoie des résultats de façon rapide et uniforme. Bien que la vitesse ne soit pas la seule mesure qui compte, [une étude de recherche sur l'expérience utilisateur](https://www.nngroup.com/articles/powers-of-10-time-scales-in-ux/) (en anglais) suggère qu'avec un temps de réponse de 0,1 seconde (100 ms), les utilisateurs ont l'impression d'interagir directement avec le système, tandis que des temps de réponse supérieurs à 1 seconde sont perçus comme un ralentissement important. Nous vous recommandons de cibler un temps de réponse d'au moins 200 ms, et préférablement de 50 ms.

Pour cela, vous devriez constamment surveiller la performance et exécuter régulièrement des tests de performance pour déterminer le temps de réponse et le débit. Voir la section [Effectuez constamment des essais](#effectuez-constamment-des-essais).

#### Limitez le débit de l'accès des utilisateurs, lorsque cela est approprié
[La limitation du débit](https://apisyouwonthate.com/blog/what-is-api-rate-limiting-all-about) (en anglais) est un bon moyen de gérer la quantité de ressources informatiques requises par une API. Si l'adoption généralisée d'une API est prévue ou si les coûts relatifs au serveur présentent une préoccupation, envisagez de limiter le débit de l'utilisateur en fonction de la fréquence à laquelle il peut lancer un appel à l'API, de la quantité de données qu'il peut demander à la fois, ou du nombre de connexions qui peuvent être actives en même temps.

La limitation du débit améliore également la sécurité en empêchant une personne malveillante de surcharger l'API en envoyant un trop grand nombre de demandes, par l'entremise d'une attaque par déni de service, tout en gardant le système disponible pour tous les utilisateurs. Si la limite est dépassée, une erreur standard HTTP 429 peut être renvoyée.

#### Mettez en œuvre la pagination et la segmentation des données
Les API qui exposent d'importants ensembles de données doivent accepter une certaine forme de segmentation des données, tant pour optimiser la performance de l'API que pour offrir une meilleure expérience à l'utilisateur. Voici quelques schémas communs de pagination, avec des cas d'utilisation appropriés :

* `page` et `per_page` sont plus appropriés lorsque l'ensemble de données n'est pas mis à jour fréquemment et les mêmes données seront probablement renvoyées pour la même référence de page avec le temps, par exemple des données historiques ou de référence.
* `offset` et `limit` sont plus appropriés pour des données fréquemment mises à jour, lorsque les utilisateurs voudront probablement voir des points de données plus anciens (décalés *offset* de) qu'un point de référence donné, par exemple pour sauter les articles de nouvelles que vous avez déjà lus.
* `since` et `limit` sont plus appropriés pour les données fréquemment mises à jour, lorsque les utilisateurs voudront probablement voir les nouveaux points de données ajoutés depuis (since) un point de référence donné, par exemple pour voir le nouveau contenu depuis votre dernière visite.

#### Appliquez des cas spéciaux aux ensembles de données en vrac
Dans certains scénarios, des API devront rendre des ensembles de données en vrac disponibles entre des systèmes ou au public. Dans ces scénarios, tenez compte des éléments suivants :

* Les plus petits ensembles de données devraient être retournés dans des formats qui nécessitent moins de temps système (p. ex., CSV ou JSON) que XML. Les pièces jointes comprimées devraient être évitées, surtout lors de l'utilisation d'API externes, car elles peuvent masquer du contenu malveillant.
* Les API de déclenchement amorcent des actions qui nécessitent beaucoup de ressources, lesquelles sont alors effectuées par un autre système. Elles peuvent commencer ou arrêter des événements tels que les transferts gérés de fichiers, ce qui est plus efficace qu'utiliser l'API pour transférer la totalité de l'ensemble de données.
* Les API recherche-et-connexion sont plus appropriés pour indexer des serveurs de fichiers existants. Ces API renvoient des liens vers des fichiers précis, et non le contenu de ces fichiers.

### Établissez une politique de mise en cache
Si votre API renvoie des données qui sont souvent demandées, mais rarement changées, vous pourriez mettre en œuvre une mémoire cache de réponse qui stocke la réponse à une demande GET dans une ressource unique pour une récupération rapide.

Meilleures pratiques en matière de mise en cache :

* Envisagez l'utilisation de [l'expiration de la mémoire cache fondée sur des clés](https://signalvnoise.com/posts/3113-how-key-based-cache-expiration-works) (en anglais) afin de ne pas servir d'objets périmés
* Assurez-vous que la mémoire cache est surveillée afin de minimiser les objets périmés
* Assurez-vous que le serveur a suffisamment de mémoire pour gérer les charges dans la mémoire cache
* Soyez prudent lors de la mise en cache de données non publiques, afin de ne pas les servir accidentellement à des utilisateurs non autorisés

### Documentation
Chaque API doit être accompagnée de documentation concise et à jour qui présente la manière de consommer cette API. Les pratiques suivantes contribuent à s'assurer que les API sont documentées correctement, sans entraîner le fardeau excédentaire associé à la gestion de documentation d'accompagnement.

#### Documentez les spécifications de l'API et les cas d'utilisation
Votre documentation devrait inclure :

* les spécifications techniques ou le contrat de l'API
* la manière dont les développeurs peuvent utiliser votre API, y compris la configuration, [l'authentification](#%C3%A9tablissez-une-politique-dacc%C3%A8s-clairement-d%C3%A9finie) et [la limitation du débit](#limitez-le-d%C3%A9bit-de-lacc%C3%A8s-des-utilisateurs-lorsque-cela-est-appropri%C3%A9)
* les renseignements concernant la disponibilité de l'API, [la gestion de version](#utilisez-la-gestion-s%C3%A9mantique-de-version) et la gestion des incidents
* un [point de contact](#faites-conna%C3%AEtre-vos-intentions-nsn-no5) et un moyen pour les utilisateurs de rester au courant des changements prévus

Un moyen efficace d'aider les utilisateurs à commencer rapidement à utiliser votre API consiste à publier du code qui l'utilise, par exemple des cas de test et des données de validation. Voir la section [Effectuez constamment des essais](#effectuez-constamment-des-essais). Des exemples de code source peuvent être publiés sur le [compte Github de la FPO](https://github.com/ongov).

#### Utilisez OpenAPI pour les API REST
Utilisez la [spécification OpenAPI](https://github.com/OAI/OpenAPI-Specification) (en anglais) pour les API REST, qui créera une spécification lisible par machine pour l'interface. Il existe des outils ouverts (p. ex., [Swagger](https://swagger.io/solutions/api-documentation/) (en anglais)) qui peuvent alors générer de la documentation lisible par l'utilisateur à partir de cette spécification, ce qui évite d'avoir à créer et à maintenir des documents distincts.

#### Langages WSDL pour SOAP
Chaque API SOAP doit être accompagné d'un contrat de langage de description de services Web ([WSDL](http://www.w3.org/TR/2007/REC-wsdl20-primer-20070626/) (en anglais)). Le langage WSDL est une spécification lisible par machine qui permet au développeur de l'API pour consommateurs de générer le code pour les consommateurs.

#### Ne documentez pas trop
En suivant le principe de « [dogfooding](#consommez-ce-que-vous-cr%C3%A9ez) », vous devriez documenter l'API dans la mesure où la documentation vous aide et aide d'autres personnes à utiliser l'API, mais pas jusqu'à ce que la documentation soit susceptible de devenir confuse et obsolète.

## Considérations futures
Un des principes sous-jacents au développement agile est que le mieux ne doit pas devenir l'ennemi du bien. Il est important d'habiliter les équipes à fournir un service solide, minimalement acceptable, qui est sécurisé, robuste et évolutif, sans devenir trop ambitieux concernant des fonctions agréables, qui retardent le lancement et empêchent de vrais utilisateurs de tester votre service. Voici d'autres facteurs dont vous devriez tenir compte lors des itérations de votre API et du développement de nouvelles fonctions.

### Utilisez un catalogue pour votre API
Toutes les API devraient être publiées avec un catalogue ou un inventaire quelconque. Un tel inventaire peut être un référentiel central de métadonnées et de documentation, un point de contact pour la gestion du cycle de vie pour les développeurs, et un portail de découverte pour les nouveaux utilisateurs. Ce catalogue peut également être intégré avec une passerelle d'API complète qui gère directement le flux du trafic de l'API, fournissant ainsi des capacités supplémentaires de gestion des utilisateurs et des contrôles de sécurité. Consultez le [Magasin des API du gouvernement du Canada](https://api.canada.ca/fr/accueil) ou le [portail des API de la NASA](https://api.nasa.gov/) pour obtenir des exemples de tels catalogues.

Contactez les Services numériques de l'Ontario pour obtenir de plus amples renseignements sur le statut d'un catalogue des API pour la Fonction publique de l'Ontario.

### Définissez une entente relative aux niveaux de service

L'idéal est que chaque API soit accompagnée d'une entente relative aux niveaux de service (ENS) claire qui définit les caractéristiques suivantes :

* Heures de soutien (p. ex., 24/7, de 9 h à 17 h, heures ouvrables d'un océan à l'autre)
* Disponibilité du service (p. ex., 99 %)
* Temps de réponse du soutien (p. ex., moins d'une heure, 24 heures, le mieux possible)
* Arrêts planifiés (p. ex., pendant la nuit, une fois par semaine, un dimanche soir sur deux)
* Limite de débit (p. ex., 100 demandes par seconde par consommateur)
* Limite sur la taille des messages (p. ex., < 1 Mo par demande)

### Publiez le code source et les tests

La publication du code source de votre API comme code source ouvert offre de nombreux avantages.

* Permet à une plus grande communauté de développeurs de repérer des problèmes potentiels avec le code
* Améliore la transparence et l'imputabilité du gouvernement
* Permet à d'autres ministères de résoudre des problèmes semblables sans devoir réinventer la roue
* Contribue à la communauté ouverte, du travail de laquelle le gouvernement bénéficie
* Démontre les compétences techniques de la fonction publique, ce qui contribue à attirer des employés talentueux

Même si vous n'avez pas l'intention d'ouvrir votre code, c'est une bonne pratique de le développer comme s'il sera examiné par le public. Cela peut souvent fournir facilement une vue d'ensemble de haut niveau qui permet de déterminer s'il y a des manques flagrants en matière de sécurité.
