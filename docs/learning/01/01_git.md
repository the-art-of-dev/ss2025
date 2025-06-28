---
marp: true
# theme: uncover
class: invert
style: |
    .logo {
        float: right;
        margin-top: 20vh;
    }
---

# Git

🌘 Git, the bright side


<img class="logo" src="../../../assets/aod-logo.svg" height="50px" />

---

## Šta je git za nas?

- Alat za verzionisanje koda
- Svaki komit predstavlja verziju
- Svaki grana predstavlja paralelnu istoriju verziju

---

## Šta naš git repozitorijum najčešće treba da sadrži?

- Kod koji je nezavistan od okruženja u kome se pokreće
- Deljene konfiguracije
- Kod koji definiše načine pokretanja sistema u određenim okruženjima

---

## Šta naš git repozitorijum najčešće NE treba da sadrži?

- Fajlove koji predstavljaju keš
- Kompajlirane fajlove ukoliko nisu third party biblioteke
- Sistemske fajlove

---

## Kloniranje repozitorijuma

- Repozitorijum najčešće ima lokalnu i udaljenu(*remote*)
- Kloniranje je proces dovlačenja udaljene verzije repozitorijuma

```bash
git clone https://github.com/the-art-of-dev/swtf.git                            # Klonira repozitorijum
cd swtf
git config pull.rebase false                                                    # Postavlja mehanizam za spajanje grana
```

---

## Kloniranje repozitorijuma sa autorizacijom | API TOKEN

- Neophodan token na git provider plaformi(npr. Github)

```bash
git clone https://<USERNAME>:<TOKEN>@github.com/the-art-of-dev/swtf.git         # Klonira repozitorijum
...
```

- Prilikom isteka ili promene tokena izmeniti token u fajlu `.git/config`

---

## Kloniranje repozitorijuma sa autorizacijom | SSH KEY

- Neophodan SSH par kljuceva
- Neophodan javni kljuc postavljen na git provider plaformi

```bash
git clone -c "core.sshCommand=ssh -i ~/SSH_PRIVATE_KEY" git@github.com:the-art-of-dev/swtf.git
```

---

## Upravljanje granama

```bash
git branch --show-current                       # Prikazuje trenutnu granu

git branch -l 'feature/*'                       # Izlistava grane sa prefixom feature/

git branch -lr '*hotfix/*'                      # Izlistava remote hotifx/ grane

git branch checkout -b feature/novi-feature     # Pravi granu feature/novi-feature

git branch checkout develop                     # Prelazi na granu develop
```

---

## Pregled loga

- Log omogućavaju lakši pregled kroz istoriju verzija

```bash
git log --oneline --decorate        # Ispisuje log verzija na trenutnoj grani

git log --stat                      # Ispisuje log verzija sa informacijama
                                    # o promenjenim fajlovima

git log -p -- libs/               # Ispisuje log verzija sa informacijama
                                    # o promenama u fajlovima u folderu libs/
```

---

## Praćenje lokalnih promena

```bash
git status -s                        # Prikazuje sve promene u repozitorijumu

git add libs/                      # Priprema sve promene iz foldera libs/ za novi komit

git restore --staged libs/test.txt # Izbacije promenu na fajlu iz pripremljenih za novi komit
```

---

## Praćenje lokalnih promena

- Fajlove koje NE treba verzionisati git-om treba dodati u `.gitignore` fajlove

  ```
  libs/ime-fajla-*
  ```

- Ukoliko je određeni fajl bio verzionisan i treba ga izbrisati

  ```bash
  git rm libs/ime-vec-verzionisanog-fajla
  ```

---

## Pravljenje komitova

```bash
git commit -m 'Poruka o komitu'     # Pravi novi lokalni komit(verziju) na osnovu pripremljenih fajlova
```

---

## Spajanje grana

```bash
git merge main      # Spaja istoriju verzija grane main u
                    # trenutnu radnu istoriju verzija i
                    # potencijalno dovodi do konflikta
```

---

## Pregled konflikata

```bash
git diff --name-only --diff-filter=U  # Lista fajlova koji sadrže konflikte

git diff --diff-filter=U              # Lista i sadrzaj fajlova koji sadrže konflikte

git diff --check                      # Lista neobrisanih konflikt markera u fajlovima
```

---

## Sinhronizacija repozitorijuma

```bash
git fetch       # Povlači nove verzije sa remote repozitorijuma

git pull        # Povlači najnoviju verziju sa trenutne grane remote repozitorijuma
                # Potencijalno dovodi do konflikta

git push        # Slanje verzija na remote server,
                # uslov je biti na poslednjoj verziji te grane
```

---
## Korisne komande

```bash
git reset --hard    # Resetovanje lokalnih promena na poslednju zapamćenu verziju (ne važi za novonastale fajlove)
git clean -fxd      # Brisanje svih fajlova koji se ne prate od strane gita(ukljucujući i novonastale)
```

---

## Paralelno verzionisanje | Izrada nove celine

- Izrada nove celine treba krene iz "čistog" lokalnog repozitorijuma

```bash
git checkout main                                   # Izdvajanje iz poslednje vrzije na main grani
git pull                                            # Povlačenje poslednje zapaćenje verzije na udaljenom repozitorijumu
git checkout -b feature/novi-feature                # Pravljenje nove grane(istorije) za izradu nove celine
git push --set-upstream origin feature/novi-feature # (NEOPHODNO PRVI PUT) Slanje nove grane na udaljeni repozitorijum
git push                                            # svaki sledeći put
```

---

## Paralelno verzionisanje | Završavanje izrade nove celine

- Završavanje izrade nove celine treba uveže poslednju istoriju u koju će se spojiti

```bash
git checkout main
git pull                                            
git reset --hard                                    # Resetuj promene logalne promene ukoliko ih ima

git checkout feature/novi-feature
git merge main                                      # Spajanje istorije main u istoriju feature/novi-feature

git diff --check                                    # Pregled konflikta ukoliko postoje

                                                    # ... rešavanje konflikta

git push                                            # Slanje spojenih verzija na remote repozitorijum
```

---

# Hvala na pažnji! 🙈 🙉 🙊

<img class="logo" src="../../../assets/aod-logo.svg" height="80px" />