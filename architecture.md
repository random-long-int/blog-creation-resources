[retour](./README.md)

# Architecture de repertoire

Il n'y a pas de conventions de nommage strictes pour les fichiers et dossiers dans une application Next.js avec TypeScript, mais voici quelques conventions couramment utilisées :

- Les fichiers de composants sont généralement nommés avec le nom du composant et l'extension .tsx (par exemple, Button.tsx, Post.tsx, Profile.tsx).
- Les fichiers de pages sont généralement nommés avec le nom de la route et l'extension .tsx (par exemple, index.tsx, [slug].tsx, login.tsx).
- Les fichiers d'API sont généralement nommés avec le nom de l'API et l'extension .ts (par exemple, like.ts, unlike.ts, comment.ts).
- Les fichiers de hook personnalisés sont généralement nommés avec le mot-clé use suivi du nom du hook et l'extension .ts (par exemple, useSupabase.ts, useCurrentSession.ts, useSession.ts).
- Les fichiers d'utils sont généralement nommés avec le nom de l'outil et l'extension .ts (par exemple, auth.ts, helpers.ts, validation.ts).

En ce qui concerne les dossiers, voici quelques conventions couramment utilisées :

- Le dossier api contient les fichiers de l'API qui sont appelés par les pages et les composants de l'application.
- Le dossier components contient les composants réutilisables de l'application.
- Le dossier hooks contient les hook personnalisés de l'application.
- Le dossier pages contient les composants de page de l'application.
- Le dossier utils contient les fichiers d'utils de l'application.

*Il est important de noter que ces conventions de nommage ne sont pas obligatoires et que vous pouvez utiliser n'importe quels noms de fichiers et de dossiers qui vous conviennent le mieux. L'important est d'être cohérent et de choisir des noms qui reflètent clairement le contenu de chaque fichier ou dossier.
Pierre-Louis Létoquart*
