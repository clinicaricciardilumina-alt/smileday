# Total Smile (allineatori) – Ricciardi Studio Dentistico

Landing per la campagna allineatori + dashboard unica per Total Lift e Allineatori.
Sito statico, nessun build: si carica così com'è su Vercel.

## File

```
index.html          landing (modulo + pagamento acconto Stripe)
grazie.html         pagina di conferma dopo il pagamento
admin/login.html    accesso staff
admin/dashboard.html dashboard unica (Total Lift + Allineatori)
assets/             foto e logo
vercel.json         indirizzi puliti (/grazie, /admin) e header di sicurezza
```

## Prima di pubblicare

1. **Link Stripe**: in `index.html` cerca `const STRIPE_LINK` e incolla il link
   di pagamento del prodotto "Acconto Allineatori".
2. **Su Stripe**, nel Payment Link → "Dopo il pagamento" → "Non mostrare la pagina di conferma,
   reindirizza al tuo sito": `https://<dominio-della-landing>/grazie`
3. **Data evento**: dalla dashboard → "Data evento" → campagna "Allineatori".

## Come funziona la dashboard unica

- Le due landing usano lo stesso Firebase (`landing-total-stripe`).
- Le prenotazioni Allineatori hanno `campagna: "allineatori"`; quelle senza campagna sono Total Lift.
- Impostazioni separate per campagna: `/config/main` (Total Lift, e password dashboard) e `/config/allineatori`.
- Login: stesse credenziali della dashboard Total Lift.

## Limiti noti (da sistemare)

- "Pagato" viene segnato quando il paziente arriva su /grazie, non da Stripe:
  controllare i pagamenti reali su Stripe. Il link passa già `client_reference_id`
  (ID prenotazione) per collegare in futuro un webhook Stripe.
- Il login è solo lato browser e il database Firestore è aperto: da proteggere
  con Firebase Authentication e regole Firestore.
