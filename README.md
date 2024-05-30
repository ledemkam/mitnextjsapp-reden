on va venir setup le projet. Pour ça, j'ai séparer le cours en 4 parties dans lesquel :

Création du projet Next.js
Setup de la base (AI + Style)
Ajout vector database
Détails
Deploy
Comme ça, on est chaud comme la braise.

Chaque fois, tu auras les "instructions" et ce que j'attends de toi, suivis de la vidéo.

1. Création du projet Next.js
Dans la première partie, nous allons venir configurer le projet. Pour cela :

Installer NextJS en suivant la documentation
Ajouter Shadcn/ui en suivant la documentation
Ajouter AI SDK en suivant le install dependencies que je t'ai partagé
Ajouter Neon en passant par le SDK
Configurer les variables d'environnement
Créer un composant ChatApp.tsx qui sera un client component pour vérifier que tout fonctionne

Solution

2. Setup de la base (AI + Style)
Le but est de setup uniquement la base de l'AI afin d'avoir un chat un peu comme ChatGPT. Le résultat final ressemble à ceci :



Ajoute le Route Handler AI (en suivant cette documentation)
Ajoute le Client Component Chat
Modifie le style de l'application avec des Card, Input et Button

Solution

3. Ajout de la Vector Database
C'est de loin la partie la plus compliquée. Si tu galères, n'hésite pas à regarder le Transcript de la vidéo solution où j'ai mis tous les bouts de code compliqués.

Ce qu'il faut faire dans cette partie est uniquement dans la route.ts. Le but va être de faire en sorte de venir query notre vector database pour récupérer le contexte.

Séparer le dernier message des autres pour récupérer le prompt de l'utilisateur
Transformer le prompt en vecteur avec OpenAI
Formater le résultat

Show less
Faire la requête pour notre database

Show less
Exécuter la requête

Show less
Formater le résultat (tu peux "log" le résultat afin de voir comment il est structuré et comment tu peux le formater)
Créer le prompt système ("Tu es NextGPT... Voici le contexte :")
Ajouter le prompt utilisateur
Récupérer la réponse OpenAI
Retourner la stream de cette réponse

Solution

4. Fignolage de l'application
On a passé le plus compliqué et maintenant on va juste ajouter quelques trucs. Le but ici va être de te faire galérer.

On a réussi le principal, maintenant c'est du pur bonus.

J'ai moi-même été en face de chaque bonus que je te présente ici et je peux te dire que ça n'a pas été facile. Voici les 4 fonctionnalités que tu dois rajouter :

1) Ajouter le contexte
Il faut étendre le flux de réponse pour ajouter le contexte à la fin sous forme de liste


Show less
2) Ajouter des boutons d'action
Si tu regardes l'API de useChat, tu verras qu'il y a des actions intéressantes. Implémente :

Stop (pour stopper l'IA)
Reset (pour réinitialiser le chat)
Reload (pour recharger la dernière réponse)
3) Ajout de l'auto-scroll
Le but est que par défaut, la page défile toute seule. MAIS si l'utilisateur veut défiler en haut, l'auto-scroll se désactive.

Quand il est désactivé, un bouton "scroll" qui le réactive apparaît.

4) Limiter l'utilisation par IP
OU demander la clé de l'utilisateur.

Pour déployer notre application, il va falloir limiter l'usage de notre application.

Pour cela, tu peux créer une fonction checkUsage côté backend qui récupère l'IP de l'utilisateur et compte les dernières requêtes qu'il a faites dans un temps donné :

TS

const searchQuery = `
SELECT COUNT(*) AS count
FROM usage
WHERE ip_address = $1 AND created_at > NOW() - INTERVAL '10 minutes';
`;
Suivant ta limite, elle lance une erreur et sinon elle ajoute une ligne dans la table usage avec l'IP de l'utilisateur.


Solution

5. Deploy
Deploy l'application sur Vercel !