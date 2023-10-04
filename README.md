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

