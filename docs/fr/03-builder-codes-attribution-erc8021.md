# Chapitre 3 -- Builder Codes : attribuer et monetiser ses transactions

`references/builder-codes/overview.md` documente l integration des Builder
Codes -- un mecanisme qui ajoute un suffixe d attribution ERC-8021 aux
donnees d appel (calldata) d une transaction, permettant a Base d attribuer
l activite a une application donnee et a son developpeur de toucher des
frais de referencement, sans modification de contrat intelligent requise.

Le prealable est d obtenir un Builder Code depuis base.dev (Settings >
Builder Codes) et d installer la librairie `ox` (`npm install ox`), qui
genere le suffixe ERC-8021.

Le workflow documente est une checklist en cinq etapes, dont l ordre
compte : d abord detecter le framework utilise par le projet (etape
obligatoire avant toute implementation), puis installer les dependances,
generer la constante `dataSuffix`, appliquer l attribution de maniere
specifique au framework detecte, et enfin verifier que l attribution
fonctionne reellement. La detection de framework se fait par lecture du
`package.json` et grep du code source (recherche de `wagmi`,
`@privy-io/react-auth`, `viem`, `ethers`, et de patterns d appel comme
`useSendCalls`/`sendCalls` pour les smart wallets ou
`useSendTransaction`/`writeContract` pour les EOA classiques), avec un
ordre de priorite explicite en cas de detection multiple : Privy avant
Wagmi avant Viem avant RPC standard. Une fois le framework identifie, la
skill impose de le confirmer explicitement aupres de l utilisateur avant
d ecrire le moindre code -- une etape de validation humaine deliberement
placee avant l implementation plutot qu apres.
