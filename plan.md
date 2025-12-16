# ACKZERO — Plan v0.1 (MVP) — Europe + UK

## 0) Positionnement (1 phrase)
ACKZERO fournit un **accusé numérique simple et indépendant** : une preuve datée et vérifiable qu’un message (contenu exact) a été **préparé**, **émis**, puis **mis à disposition** à une date/heure donnée — sans se substituer à un recommandé électronique.

## 1) Problème réel
- Email classique : facile de contester (“je n’ai rien reçu”, “ce n’est pas le bon contenu”, “c’était un brouillon”, “la date est falsifiable”).
- Recommandé électronique / eIDAS : souvent lourd, coûteux, friction (identité, parcours long, usages pro, etc.).
- Besoin terrain (consommateurs + TPE/PME) : résiliation, litige, RH, freelance, assurance, SAV.

## 2) Ce que prouve ACKZERO (exactement)
### 2.1 “Proof of Content”
- Preuve que **ce contenu exact** (hash) existait au moment T.
- Permet de prouver *ce qui a été écrit*, pas seulement “un email envoyé”.

### 2.2 “Proof of Emission”
- Preuve que l’utilisateur a déclenché une **émission** vers une cible (email ou URL de dépôt), à T.
- Preuve technique (horodatage + receipt serveur), et *optionnellement* preuve SMTP si on passe par un relais.

### 2.3 “Proof of Availability”
- Preuve que le message a été **mis à disposition** via une page publique/un lien unique (ou coffre public) à T.
- Utile même si le destinataire nie l’avoir lu.

### 2.4 Ce que ACKZERO **ne** prouve pas (à afficher clairement)
- Ne prouve pas que la personne a **ouvert** / **lu** (sauf mécanisme d’acceptation volontaire).
- Ne remplace pas un **recommandé électronique qualifié** (eIDAS).  
- Ne “force” pas une valeur juridique universelle : c’est une **preuve technique** de contenu + temps + disponibilité.

## 3) MVP v0.1 — Objectif
- **Utilisation en < 60 secondes**, sans compte.
- Une page web simple :
  1) l’utilisateur colle son message (ou importe un PDF)
  2) saisit l’email destinataire (optionnel selon mode)
  3) génère une **preuve** + un **lien de vérification**
  4) copie/colle dans son email ou envoie via ACKZERO (selon mode)
- La preuve est **vérifiable publiquement** (sans login).

## 4) Modes d’usage (v0.1)
### Mode A — “Copy/Paste” (zéro intégration)
- L’utilisateur écrit son message sur ACKZERO.
- ACKZERO génère :
  - un **Receipt** (JSON + PDF)
  - un **code** / **lien de vérification** à insérer dans l’email envoyé depuis sa boîte habituelle.
- Avantage : ultra simple, compatible partout.
- Limite : ACKZERO ne prouve pas techniquement l’envoi SMTP, seulement le contenu + l’intention + la mise à disposition (si page publique).

### Mode B — “Send via ACKZERO relay” (option v0.1 si simple)
- L’utilisateur écrit sur ACKZERO + indique destinataire.
- ACKZERO envoie l’email via un relais (SMTP/Provider).
- ACKZERO fournit un reçu d’émission (message-id, horodatage, logs minimaux).
- Avantage : preuve d’émission plus forte.
- Limite : complexité + conformité (anti-abus, délivrabilité).  
**Recommandation pragmatique** : commencer par Mode A en v0.1, ajouter Mode B en v0.2.

## 5) Preuve & format (v0.1)
### 5.1 Données minimales du Receipt (JSON)
- `spec`: "ackzero.v0.1"
- `issued_at`: timestamp ISO UTC
- `content_hash`: sha256 du contenu normalisé
- `subject` (optionnel)
- `to`: email (optionnel / ou hash de l’email si on veut minimiser)
- `method`: "copy_paste" | "relay"
- `availability_url`: lien public de consultation (optionnel, recommandé)
- `receipt_id`: identifiant court
- `signature`: signature serveur (ou attestation)
- `verify_url`: URL publique de vérification

### 5.2 PDF “receipt”
- Un PDF simple lisible par un juge / RH / assureur :
  - identifiant
  - date UTC + date locale
  - hash
  - résumé (non sensible) + lien verify
  - note “ce que cela prouve / ne prouve pas”

### 5.3 Normalisation du contenu (important)
- UTF-8, normalisation des fins de ligne, trim stable.
- Option : inclure aussi le hash de la pièce jointe si fichier.

## 6) UX v0.1 (1 page)
Sections recommandées :
1) Hero : “Generate a verifiable receipt in 60s”
2) Form : Subject + Message + Optional recipient email
3) Bouton : “Generate Receipt”
4) Résultat :
   - Verify link
   - Receipt JSON download
   - Receipt PDF download
   - “Insert this line in your email:” (lien + receipt_id)
5) “What this proves / doesn’t prove” (clair, court)
6) Pricing v0.1 (simple) + Contact

## 7) Monétisation v0.1 (simple, sans compte)
- **Pay-per-receipt** (Stripe Payment Link) : ex. 2–5€ / reçu
- Pack 10 / 50 reçus (pour pros) via paiement unique.
- Après paiement : délivrer un “token de génération” dans l’URL (ou code).
**Non-critique v0.1** : abonnement, dashboard, historique.

## 8) Anti-abus & sécurité (obligatoire)
- Rate limiting IP
- Captcha léger si abus
- Filtrage contenu : interdits (harcèlement, doxxing, menaces, etc.)
- Journaux minimaux et rétention courte
- Protection contre usage spam si Mode B (relay)
- `security.txt` + contact abuse

## 9) RGPD / Privacy (obligatoire)
- Minimiser les données :
  - idéalement stocker uniquement hash + métadonnées minimales
  - éviter stockage du contenu brut (ou stockage chiffré + expiration)
- Politique de conservation : courte, claire.
- Consentement explicite si email destinataire stocké/traité.

## 10) Différenciation vs alternatives
- Plus simple qu’e-recommandé qualifié : pas de KYC, pas de lourdeur.
- Plus solide qu’un email seul : hash, horodatage, vérification publique.
- Focus : **preuves pratiques** pour litiges du quotidien.

## 11) Roadmap après v0.1
### v0.2
- Mode B (relay) si délivrabilité maîtrisée
- “Recipient acknowledgement” volontaire : page “I acknowledge receipt” (option)
- Packs pro + clé API (option)
- Amélioration PDF + templates de lettres (mutuelle, assurance, etc.)

### v1.0
- Comptes pro + espace d’historique (si traction)
- SLA + support
- Intégrations (Gmail add-on / Outlook add-in) si justifié

## 12) Ce qui est NON critique (à ne pas faire en v0.1)
- Dashboard complet
- Auth/inscription
- Abonnements mensuels
- Intégrations lourdes (addons)
- “Lecture prouvée” par tracking invisible (à éviter)

## 13) Définition of Done v0.1
- Génération receipt JSON + PDF
- Lien verify public
- Normalisation + hash stable
- Anti-abus minimal (rate limit)
- Pages légales minimales (privacy/terms)
- Parcours utilisateur < 60s, mobile OK
- Explication “prouve / ne prouve pas” extrêmement claire

## 14) Message clé (à marteler)
“Une date d’email ne suffit pas. ACKZERO fournit une preuve indépendante : **contenu exact + horodatage + vérification publique**.”
