# SP1 Kroužky

Kód žáka: K07

## Co bolí na původní tabulce
* Kroužek, vedoucí, den, místnost a cena se opakují u každé přihlášky. Když Robotika zdraží, musím přepisovat čtyři řádky[cite: 1].
* Stejná věc je pokaždé napsaná jinak: názvy kroužků (Robotika / robotika / ROBOTIKA), vedoucích (Horák / Mgr. Horák / Horak) i formát ceny (600 / 600 Kč)[cite: 1].
* „Kolik kroužků škola nabízí?“ z tabulky spolehlivě nezjistím, protože názvy kroužků jsou psané různými způsoby a splývají s přihláškami[cite: 1].

## Tabulky a klíče

### zaci.csv
* **PK:** `id_zaka`

| id_zaka | jmeno | prijmeni | trida |
| :--- | :--- | :--- | :--- |
| 1 | Adam | Novák | IT2 |
| 2 | Eva | Nováková | IT2 |
| 3 | Jan | Procházka | IT2 |
| 4 | Eliška | Kučerová | IT2 |
| 5 | Petr | Dvořák | IT2 |
| 6 | Tomáš | Svoboda | IT2 |

### krouzky.csv
* **PK:** `id_krouzku`

| id_krouzku | nazev | vedouci | den | cas | mistnost | cena_kc |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Robotika | Mgr. Horák | čt | 14:00 | 13 | 600 |
| 2 | Fotografie | Veselá | út | 15:00 | 210 | 450 |
| 3 | Šachy | Ing. Beneš | po | 14:00 | 207 | 300 |
| 4 | 3D tisk | Král | st | 14:00 | 13 | 800 |

### prihlasky.csv
* **PK:** `id_prihlasky`
* **FK:** `id_zaka` → `zaci`
* **FK:** `id_krouzku` → `krouzky`

| id_prihlasky | id_zaka | id_krouzku | zaplaceno |
| :--- | :--- | :--- | :--- |
| 1 | 1 | 1 | ano |
| 2 | 2 | 2 | ano |
| 3 | 3 | 1 | ne |
| 4 | 4 | 3 | ano |
| 5 | 1 | 3 | ano |
| 6 | 5 | 4 | ano |
| 7 | 6 | 1 | ano |
| 8 | 4 | 2 | ne |
| 9 | 5 | 1 | ano |
| 10 | 2 | 4 | ano |
| 11 | 3 | 3 | ano |
| 12 | 6 | 2 | ne |

## ER diagram

```mermaid
erDiagram
    ZAK ||--o{ PRIHLASKA : má
    KROUZEK ||--o{ PRIHLASKA : obsahuje

    ZAK {
        int id_zaka PK
        string jmeno
        string prijmeni
        string trida
    }

    KROUZEK {
        int id_krouzku PK
        string nazev
        string vedouci
        string den
        string cas
        string mistnost
        int cena_kc
    }

    PRIHLASKA {
        int id_prihlasky PK
        int id_zaka FK
        int id_krouzku FK
        string zaplaceno
    }
