<div align="center"><img src="./docs/images/charonlogo.svg" /></div>
<h1 align="center">Charon<br/>Der verteilte Validator-Middleware-Client</h1>

<p align="center"><a href="https://github.com/obolnetwork/charon/releases/"><img src="https://img.shields.io/github/tag/obolnetwork/charon.svg"></a>
<a href="https://github.com/ObolNetwork/charon/blob/main/LICENSE"><img src="https://img.shields.io/github/license/obolnetwork/charon.svg"></a>
<a href="https://godoc.org/github.com/obolnetwork/charon"><img src="https://godoc.org/github.com/obolnetwork/charon?status.svg"></a>
<a href="https://goreportcard.com/report/github.com/obolnetwork/charon"><img src="https://goreportcard.com/badge/github.com/obolnetwork/charon"></a>
<a href="https://github.com/ObolNetwork/charon/actions/workflows/golangci-lint.yml"><img src="https://github.com/obolnetwork/charon/workflows/golangci-lint/badge.svg"></a></p>

Dieses Repo enthält den Quellcode für den verteilten Validator-Client _Charon_ (ausgesprochen 'kharon'); ein HTTP-Middleware-Client für Ethereum Staking, der es Ihnen ermöglicht, einen einzelnen Validator sicher über eine Gruppe unabhängiger Nodes laufen zu lassen.

Charon wird von einer Webapp namens [Distributed Validator Launchpad] (https://goerli.launchpad.obol.tech/) für die Erstellung verteilter Validierungsschlüssel begleitet.

Charon wird von Stakern verwendet, um die Verantwortung für die Ausführung von Ethereum-Validatoren auf eine Reihe von verschiedenen Instanzen und Client-Implementierungen zu verteilen.

![Example Obol Cluster](./docs/images/DVCluster.png)

###### Ein verteilter Validator-Cluster, der den Charon-Client zur Absicherung von Client- und Hardware-Ausfallrisiken verwendet

## Schnellstart

Der einfachste Weg, Charon zu testen, ist mit dem [charon-distributed-validator-cluster](https://github.com/ObolNetwork/charon-distributed-validator-cluster) Repo
das ein Docker-Compose-Setup enthält, um einen vollständigen Charon-Cluster auf Ihrem lokalen Rechner zu betreiben.

## Dokumentation

Die Website [Obol Docs](https://docs.obol.tech/) ist der beste Platz für den Einstieg.
Die wichtigsten Abschnitte sind [intro](https://docs.obol.tech/docs/intro),
[Schlüsselkonzepte](https://docs.obol.tech/docs/int/key-concepts) und [Charon](https://docs.obol.tech/docs/dv/introducing-charon).

Eine ausführliche Dokumentation zu diesem Repo finden Sie im Ordner [docs](docs):

- [Konfiguration](docs/configuration.md): Einen Charon-Knoten konfigurieren
- [Architektur](docs/architecture.md): Überblick über den Charon-Cluster und die Node-Architektur
- [Projektstruktur](docs/structure.md): Struktur der Projektordner
- [Verzweigungs- und Freigabemodell](docs/branching.md): Git Verzweigungs- und Freigabemodell
- [Go-Richtlinien](docs/goguidelines.md): Richtlinien und Grundsätze für die Entwicklung von Go
- [Beitragen](docs/contributing.md): Wie man zu Charon beiträgt; Githooks, PR-Vorlagen, usw.

Es gibt immer die [charon godocs](https://pkg.go.dev/github.com/obolnetwork/charon) für die Quellcode-Dokumentation.

## Unterstützte Konsensschicht-Clients

Charon integriert sich in den Ethereum-Konsensus-Stack als Middleware zwischen dem Validator-Client
und dem Beacon-Knoten über die offizielle [Eth Beacon Node REST API] (https://ethereum.github.io/beacon-APIs/#/).
Charon unterstützt jeden Upstream Beacon Node, der die Beacon API bedient.
Charon zielt darauf ab, jeden nachgelagerten Standalone-Validator-Client zu unterstützen, der die Beacon-API nutzt.

| Client                                             | Beacon Node | Validator-Client | Anmerkungen                                   |
| -------------------------------------------------- | :---------: | :--------------: |-----------------------------------------|
| [Teku](https://github.com/ConsenSys/teku)          |     ✅      |        ✅        | Vollständige Unterstützung                        |
| [Lighthouse](https://github.com/sigp/lighthouse)   |     ✅      |        ✅        | Vollständige Unterstützung                        |
| [Lodestar](https://github.com/ChainSafe/lodestar)  |     ✅      |       \*️⃣        | Problem der DVT-Kompatibilität                 |
| [Vouch](https://github.com/attestantio/vouch)      |     \*️⃣     |        ✅        | Nur Validator-Client bereitgestellt          |
| [Prysm](https://github.com/prysmaticlabs/prysm)    |     ✅      |        🛑        | Validator-Client erfordert gRPC-API      |
| [Nimbus](https://github.com/status-im/nimbus-eth2) |     ✅      |        ✅        | Demnächst auch unterstützt |

## Status des Projekts

Das Obol-Netzwerk befindet sich noch im Anfangsstadium, und die Entwicklung ist noch nicht abgeschlossen.
Wir kommen schnell voran, also schauen Sie regelmäßig vorbei, um die Fortschritte zu verfolgen.

Charon ist ein verteilter Validator, d.h. seine Hauptaufgabe ist die Durchführung von Validierungsaufgaben.
Die folgende Tabelle zeigt, welche Clients welche Aufgaben in einem öffentlichen Testnetz erbracht haben und welche sich noch im Aufbau befinden (🚧 )

| Dienst  \ Client                        |                      Teku                      |                    Lighthouse                    | Lodestar | Nimbus|Vouch | Prysm |
|--------------------------------------|:----------------------------------------------:|:------------------------------------------------:|:--------:|:------:|:-----:|:-----:|
| _Attestation_                        |                       ✅                        |                        ✅                         |    🚧    |   🚧   |  ✅   |  🚧   |
| _Attestation Aggregation_            |                       🚧                       |                        🚧                        |    🚧    |   🚧   |  🚧   |  🚧   |
| _Block Proposal_                     |                       ✅                        |                        ✅                         |    🚧    |   🚧   |  🚧   |  🚧   |
| _Blinded Block Proposal (mev-boost)_ | [✅](https://ropsten.beaconcha.in/block/555067) | [✅](https://ropsten.etherscan.io/block/12822070) |    🚧    |   🚧   |  🚧   |  🚧   |
| _Sync Committee Message_             |                       ✅                        |                        ✅                         |    🚧    |   🚧   |  🚧   |  🚧   |
| _Sync Committee Contribution_        |                       🚧                       |                        🚧                        |    🚧    |   🚧   |  🚧   |  🚧   |
