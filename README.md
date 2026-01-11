# AgroPrice Insight

Kratak opis sistema za automatsko preuzimanje, skladištenje i vizuelizaciju mesečnih indeksa cena proizvođača poljoprivrednih proizvoda.

## 1. Opis projekta
AgroPrice Insight omogućava automatsko preuzimanje i analizu podataka sa zvaničnog Open Data API-ja Srbije:

https://opendata.stat.gov.rs/data/WcfJsonRestService.Service1.svc/dataset/03020203IND01/1/json

Sistem pruža:
- Dashboard vizuelizacije
- API sloj
- Automatsku sinhronizaciju
- Izveštaje
- Administraciju

## 2. Glavne funkcionalnosti
- Automatski import podataka
- Grafički prikaz trendova
- Filtriranje po periodima i grupama proizvoda
- PDF/Excel izveštaji (planirano)
- REST API za integracije
- Administratorski panel

## 3. Tehnologije
- Backend: Node.js / Express
- Frontend: React + TypeScript
- Baza: PostgreSQL
- Deploy: Docker

## 4. Struktura projekta
/docs – AI_TEMPLATE dokumenti  
/backend – API i ETL  
/frontend – dashboard aplikacija  

## 5. Brzi start

### Backend
```
cd backend
npm install
npm run dev
```

### Frontend
```
cd frontend
npm install
npm run dev
```

## 6. AI_TEMPLATE integracija
(https://github.com/inter-coder/AI_TEMPLATE)
Dokumentacija se vodi u sledećim fajlovima:
- CLAUDE.md  
- PROJECT_DIRECTOR.md  
- DIRECTOR_OF_DEVELOPMENT.md  
- DEVELOPMENT_TEAM.md  
- PROJECT_STATUS.md  

## 7. Kontakt
Softverska kuća – Symappsys DOO.
https://symappsys.com