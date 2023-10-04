# Bradlo Attack & Defense

## Za co lze získat / ztratit body?

### 1. Infrastruktura v Kubernetes clusteru

Je pro vás připraven Kubernetes cluster, který obsahuje následující služby o jejiž dostupnost se musíte postarat.

Kontrola probíhá každou minutu a v případě, že služba bude nedostupná nebo vráti špatný výsledek, tak se týmu odečte 1
bod.

Každý tým má separátní cluster, ke kterému přistupuje přes kubeconfig, který jim bude přidělen při startu cvičení. Dále
jsou týmu přiděleny 2 A DNS záznamy pro přístup ke službám pinguin a facebug.

> Kubeconfig naleznete na [https://static.haxagon.xyz/heslo-tymu](https://static.haxagon.xyz/heslo-tymu)


Tyto DNS záznamy jsou:

- team **Moře**:
    - [pinguin](http://pinguin.team1.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team1.bradlo.testing.haxagon.xyz)
- team **Ouagadougou**:
    - [pinguin](http://pinguin.team2.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team2.bradlo.testing.haxagon.xyz)
- team **phoenix**:
    - [pinguin](http://pinguin.team3.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team3.bradlo.testing.haxagon.xyz)
- team **Raptoři 🦖**:
    - [pinguin](http://pinguin.team4.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team4.bradlo.testing.haxagon.xyz)
- team **SVN**:
    - [pinguin](http://pinguin.team5.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team5.bradlo.testing.haxagon.xyz)
- team **Neposlouchám hip-hop**:
    - [pinguin](http://pinguin.team6.bradlo.testing.haxagon.xyz)
    - [facebug](http://facebug.team6.bradlo.testing.haxagon.xyz)

#### 1.1. Pinguin

Jednoduchá služba pro monitorování dostupnosti webových stránek.
Na URL adrese `http://pinguin.team<ID týmu>.bradlo.testing.haxagon.xyz/ping` přijímá HTTP POST request s JSON payloadem
ve formátu: `{"domain": "root.cz"}`. Server následně zkontroluje dostupnost zadané domény a vrátí výstup programu ping.

Příklad odpovědi:

```json
{
  "result": "PING root.cz (91.213.160.188) 56(84) bytes of data.\n64 bytes from 91.213.160.188 (91.213.160.188): icmp_seq=1 ttl=54 time=14.6 ms\n\n--- root.cz ping statistics ---\n1 packets transmitted, 1 received, 0% packet loss, time 0ms\nrtt min/avg/max/mdev = 14.615/14.615/14.615/0.000 ms\n"
}
```

Dostupnost této služby je automaticky kontrolována požadavkama s náhodnou doménou. Kontroluje se, zdali výsledek
odpovědi
koresponduje s očekávatelnou odpovědí na ping této domény.

[Source Code](https://github.com/david-sykora/pinguin)

#### 1.2. Facebug

Jednoduchá služba pro vyhledávání osob podle jména a příjmení. Očekává se, že aplikace dokáže zpracovat GET požadavek
ve formátu `http://facebug.team<ID týmu>.bradlo.testing.haxagon.xyz/search?firstName=Amanda&lastName=Wilson`

Očekává se JSON odpověď ve formátu:

```json
{
  "result": [
    {
      "id": 11,
      "firstName": "Amanda",
      "lastName": "Wilson"
    }
  ]
}
```

Je třeba aby byl zachován přesný stav databáze, který je pro cvičení připraven.

[Source Code](https://github.com/david-sykora/facebug)

### 2. Kačena

Kačena je předmět. Tento předmět je velmi vzácný. Tento vzácný předmět je úkolem najít. V momentě, kdy ho tým najde, tak
se k němu připojí pomocí Ethernetu. V případě jedné kačeny se dokonce musí nakrimpovat konektor RJ45.

Aby se síťová komunikace s kačenou mohla navázat, tak jí musíte pomocí DHCP nabídnout IP adresu. Tento DHCP server
musíte pochopitelně spustit na svém počítači... Potom co bude kačena dostupná na síti, tak se k ní připojíte pomocí SSH.
Přístupové údaje na SSH jsou pro obě kačeny:

- username: challenger
- password: zadek

Po přihlášení na SSH se otevře textový editor. Upravte otevřený soubor, aby obsahoval pouze ID vašeho týmu. Od tohoto
okamžiku bude kačena každou minutu připisovat 5 bodů týmu jekož ID je uloženo v kačeně.

Ale pozor! Kačena je nerada daleko od svého domečku - terasy před jídelnou. Pokud se vzdálí příliš, tak začne hlasitě
nadávat a přestane přičítat body!

Pravidla:

- Zákaz manipulace s jinými fyzickými porty, než je síťový RJ45 (u krimpovací kačeny je dovoleno pouze manipulovat s
  nenakrimpovaných UTP kabelem)
- Zákaz ovládání reproduktoru kačeny
- Zákaz umisťování kačeny do těžko dostupných míst
- V případě, že kačena vykazuje chybové chování, tak neprodleně závadu nahlašte

Do kačen zapisujte tyto idetifikátory týmů:
- team **Moře**: `6519c6bc3cee6044542a196e`
- team **Ouagadougou**: `6519c6bc3cee6044542a196d`
- team **phoenix**: `6519c6bc3cee6044542a196c`
- team **Raptoři 🦖**: `6519c6bc3cee6044542a196b`
- team **SVN**: `6519c6bc3cee6044542a196a`
- team **Neposlouchám hip-hop**: `6519c6bc3cee6044542a1969`

### 3. Tickets

Tickety neboli papirky jsou digitální prolnutí s fyzickou realitou.
V terénu jsou rozmístěni papírky různé hodnoty. Tato hodnota je znázorněna barvou:

- hnědá: 10
- zelená: 20
- modrá: 30
- červená: 60
- černá: 120

Každý papírek má kromě barevného znázornění na sobě i alfanumerický kód. V prohlížeči otevřte odevzdávací portál, na
portálu vyberte svůj tým a do textového vstupu zadejte kód z papírku. Poté bude vybranému týmu přičten daný počet bodů.
Každý papírek lze použít pouze jednou.

Odevzdávací portál je dostupný na adrese: https://bradlo.testing.haxagon.xyz/static/ticket-machine.html

Vyberte v něm prosím svůj tým a vyplňte secret z papírku.

[Mapa rozmístění](https://static.haxagon.xyz/map.png)

### 4. Analfabetova výzva

Vyzvěte Analfabeta v souboji o rychlost. Před jídelnou vyhledejte Sama s Bárou.

### 5. Casino Las Vegas

Přijď do lobby za Filipem & Alanem znásobit svoje body nebo prohrát kalhoty.

### 6. Sportovní šampion

U Filipa & Alana se můžeš stát šampionem sportu. Vyzvi jiný tým na souboj v některém ze sportů až vyhraj **100 bodů**.

### 7. Cháron

Obstojíš před Cháronem? Pokud ano, získáš **300 bodů**. U bazénu najdi Sama.
