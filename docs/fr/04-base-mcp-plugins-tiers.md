# Chapitre 4 -- Base MCP : un wallet pour l agent, et des plugins tiers gates par nom

`base-mcp` donne a l assistant IA acces a un Base Account via le serveur MCP
hosted sur `mcp.base.org` -- portefeuille, portfolio, envoi, swap, signature,
paiements x402, appels de contrat groupes, et historique de transactions.
Le fichier impose un rituel d "Onboarding" court mais obligatoire en debut
de conversation des que Base MCP est concerne : mentionner brievement les
capacites disponibles sans enumerer tous les outils, afficher un
disclaimer legal verbatim (les plugins tiers ne sont ni operes ni audites
par Base, les transactions sont irreversibles), et ne recuperer l adresse
du wallet ou son solde que si l utilisateur le demande explicitement ou
qu une operation en attente en a reellement besoin -- jamais par defaut.

Le catalogue d outils lui-meme n est pas fige dans la documentation : la
skill precise explicitement que l agent doit lire le catalogue expose
dynamiquement par le serveur MCP (source de verite qui peut changer), et ne
jamais precharger une liste fixe depuis ce fichier.

Le point le plus structurant est la regle de routage des plugins tiers
(Aerodrome, Uniswap, Moonwell, Morpho, OpenSea, et une vingtaine d autres,
chacun couvrant DeFi, swaps, NFT, ou inference IA) : un plugin ne doit
etre ouvert que lorsque l utilisateur nomme explicitement la plateforme
tierce concernee ("swap sur Uniswap", "preter sur Moonwell") -- jamais par
inference automatique a partir d une simple capacite demandee ("swap des
USDC", "gagner du rendement"). Si l utilisateur demande une capacite sans
nommer de plateforme, l agent doit lister les options disponibles dans le
tableau et laisser l utilisateur choisir, plutot que de decider a sa place
quel service tiers utiliser -- une decision jugee trop consequente pour
etre automatisee, puisqu elle engage la confiance et les fonds de
l utilisateur envers un tiers precis.
