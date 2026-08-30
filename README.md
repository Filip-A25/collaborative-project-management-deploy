# Collaborative Project Management App Deployment

Repozitorij sadrži konfiguraciju za deployment Collaborative Project Management aplikacije koja uključuje
.NET 9.0 API, SQL Server bazu podataka i Next.js 16 klijentski sloj. Ovaj repozitorij služi kao središnja
točka za pokretanje cjelokupne aplikacije.

Kod same aplikacije nalazi se u pojedinačnim repozitorijima:

- [collaborative-project-management-backend](https://github.com/Filip-A25/collaborative-project-management-backend) - .NET API (SQL Server baza)
- [collaborative-project-management-frontend](https://github.com/Filip-A25/collaborative-project-management-frontend) - Next.js klijentski sloj

## Preduvjeti za pokretanje

- [Docker](https://docs.docker.com/get-started/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install)

## Konfiguracija

| Varijable okruženja | Opis                                                   | Primjer                   |
| ------------------- | ------------------------------------------------------ | ------------------------- |
| `MSSQL_PASSWORD`    | Lozinka baze podataka za korisnika `sa`                | `CPMApiPassword000!`      |
| `JWT_SECRET`        | Niz znakova za potpisivanje tokena                     | `strong-generated-string` |
| `API_URL`           | Endpoint na koji klijentski sloj šalje zahtjeve na API | `http://api:8080/api/v1`  |

Napomena: `api:8080` označava ime `service` API-ja u `compose.yaml`

## Upute za pokretanje

Prije samog pokretanje potrebno je klonirati sva tri repozitorija lokalno:

- [collaborative-project-management-backend](https://github.com/Filip-A25/collaborative-project-management-backend)
- [collaborative-project-management-frontend](https://github.com/Filip-A25/collaborative-project-management-frontend)
- [collaborative-project-management-deploy](https://github.com/Filip-A25/collaborative-project-management-deploy)

```bash
# Klonirajte repozitorije
git clone https://github.com/Filip-A25/collaborative-project-management-backend.git
git clone https://github.com/Filip-A25/collaborative-project-management-frontend.git
git clone https://github.com/Filip-A25/collaborative-project-management-deploy.git
```

Premjestite `api` (backend) i `frontend` direktorije unutar `deploy` direktorija. Dakle, `deploy` direktorij
treba biti korijenski direktorij projekta. Nazivi direktorija moraju biti identični nazivima za `service`
unutar `compose.yaml` (`api` i `frontend`).

```bash
# Prikaz ispravne strukture direktorija
collaborative-project-management-deploy/
├── api/
├── frontend/
├── compose.yaml
├── .env.example
├── .gitignore
└── README.md
```

Zatim stvorite `.env` datoteku unutar korijenskog direktorija s varijablama okruženja na temelju `.env.example`.

```bash
# Pokrenite izgradnju slike iz Dockerfile-a i pokrenite Docker containere
docker compose up -d --build
```
