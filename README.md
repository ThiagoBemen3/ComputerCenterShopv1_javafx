# ComputerCenterShop — pràctica integradora RA2

> **Plantilla de l'equip.** Copieu aquest fitxer al vostre repositori de treball i completeu-lo a mesura que avanceu. No inclou solucions de codi: les decisions, proves i explicacions han de ser vostres.

## Fitxa de l'equip

- Integrants: **Alex Alcaraz Castillo** i **Thiago Prieto Calvo**
- Repositori compartit: **https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx**
- Branca de treball habitual: **main**
- Data d'inici: **2026-11-12**
- Última actualització: **2026-11-24**

## Propòsit del projecte

En aquesta pràctica desenvolupem una aplicació Java que accedeix a una base de dades relacional amb JDBC. Treballem sobre el projecte *starter* indicat pel professorat i fem servir el backlog RA2 per organitzar les tasques, els commits, les proves i les decisions tècniques.

El repositori ha de mostrar el procés de treball real de l'equip. No es tracta només d'arribar a una aplicació que s'executi: també cal poder explicar què s'ha canviat, com s'ha comprovat i per què la decisió correspon a cada *issue*.

## Punt de partida

- Repositori *starter* utilitzat: **ComputerCenterShop_v1_javafx_starter (facilitat pel professorat)**
- Gestor de base de dades relacional utilitzat: **H2 Database, en mode fitxer local (sense servidor)**
- Connector utilitzat: **H2 JDBC, `com.h2database:h2:2.2.224`, declarat al `pom.xml`**
- Entorn de desenvolupament: **Eclipse 2026-09 amb Maven integrat (m2e) i Java 25**
- Comandament o acció que fem servir per comprovar l'execució: **a Eclipse, clic dret a `src/main/Ra2JdbcDemo.java` → Run As → Java Application**

> No incorporeu ORM, Hibernate, ObjectDB, MongoDB, serveis externs ni persistència principal en fitxers. Aquests elements no formen part de RA2.

## Com treballem cada *issue*

1. Llegim l'objectiu i els criteris d'acceptació de l'*issue*.
2. Acordem què ha de canviar i qui inicia la feina.
3. Fem canvis petits i comprensibles, amb *commits* que expliquin la decisió.
4. Provem el comportament esperat i en guardem una evidència.
5. Actualitzem aquest README amb el resultat, la prova i l'enllaç al *commit* o a la *pull request*.
6. Tanquem l'*issue* només quan l'equip pot explicar individualment la solució aplicada.

## Progrés del backlog

Marqueu una tasca quan la prova i el rastre al repositori estiguin recollits. Els enllaços apunten a l'enunciat, no a una solució.

### M1 · Base JDBC operativa

- [X] [RA2-ISSUE-01 · Preparar el projecte JDBC](issues/RA2-ISSUE-01-preparar-projecte-jdbc.md)
- [X] [RA2-ISSUE-02 · Connector, URL i connexió](issues/RA2-ISSUE-02-revisar-connector-url-connexio.md)
- [X] [RA2-ISSUE-03 · Estructura relacional](issues/RA2-ISSUE-03-crear-estructura-relacional.md)

### M2 · Operacions relacionals principals

- [X] [RA2-ISSUE-04 · Inserció de dades](issues/RA2-ISSUE-04-inserir-producte-preparedstatement.md)
- [ ] [RA2-ISSUE-05 · Actualització d'estoc](issues/RA2-ISSUE-05-actualitzar-estoc.md)
- [X] [RA2-ISSUE-06 · Eliminació controlada](issues/RA2-ISSUE-06-eliminar-producte-controlat.md)
- [ ] [RA2-ISSUE-07 · Consultes i resultats](issues/RA2-ISSUE-07-consultar-inventari-resultset.md)

### M3 · Robustesa JDBC

- [ ] [RA2-ISSUE-08 · Tancament de recursos](issues/RA2-ISSUE-08-tancar-recursos.md)
- [ ] [RA2-ISSUE-09 · Transaccions](issues/RA2-ISSUE-09-transaccio-commit-rollback.md)
- [ ] [RA2-ISSUE-10 · Procediment amb paràmetres](issues/RA2-ISSUE-10-procediment-parametres.md)
- [ ] [RA2-ISSUE-11 · Errors de connexió i operacions](issues/RA2-ISSUE-11-errors-connexio-recursos.md)

### M4 · Documentació i tancament

- [ ] [RA2-ISSUE-12 · Documentar l'execució i la configuració](issues/RA2-ISSUE-12-documentar-execucio-configuracio.md)
- [ ] [RA2-ISSUE-13 · Preparar el lliurament de la pràctica](issues/RA2-ISSUE-13-lliurament-practica-integradora.md)

## Registre de treball

Dupliqueu aquest bloc per a cada *issue* que completeu. Escriviu amb les vostres paraules i enllaceu només proves i *commits* del vostre repositori.

### RA2-ISSUE-XX · [títol de l'*issue*]

- Estat: **pendent | en curs | comprovat**
- Persona que l'ha iniciat: **[nom]**
- Problema inicial: **[què no funcionava o què faltava]**
- Decisió aplicada: **[què heu decidit fer i per què]**
- Canvis fets: **[fitxers o parts del projecte modificades]**
- Prova realitzada: **[cas que heu provat i resultat observat]**
- Evidència: **[enllaç a captura, registre, vídeo breu o apartat del repositori]**
- *Commit* o *pull request*: **[enllaç o identificador]**
- Explicació individual: **[què pot explicar cada integrant sobre aquesta tasca]**
- Ús d'IA, si n'hi ha hagut: **[consulta feta, ajuda rebuda i comprovació pròpia]**

### RA2-ISSUE-02 · Connector, URL i connexió

- Estat: **comprovat**
- Persona que l'ha iniciat: **Thiago**
- Problema inicial: **el mètode `connect()` no obria cap connexió. Llançava l'error «RA2-ISSUE-02 pendent» i la demo s'aturava abans d'arribar a la base de dades.**
- Decisió aplicada: **obrir la connexió amb `DriverManager.getConnection(url, user, password)` i guardar-la al camp `conn`, perquè la puguin fer servir la resta de mètodes. Mantenim la lectura de les propietats de sistema (`computercenter.db.url`, `computercenter.db.user` i `computercenter.db.password`) per poder canviar la configuració sense modificar el codi. Si no s'indiquen, es fa servir H2 local.**
- Canvis fets: **`src/dao/ProductDaoImplJDBC.java`, mètode `connect()`: hem tret el TODO i el `throw pending(...)` i hem afegit la crida a `DriverManager`. No ha calgut tocar el `pom.xml` perquè ja incloïa H2.**
- Prova realitzada: **en executar `Ra2JdbcDemo` ja no surt «RA2-ISSUE-02 pendent». Ara s'atura a «RA2-ISSUE-03 pendent», que és el pas següent, i es crea el fitxer `data/computercenter_v1_starter.mv.db`.**
- Evidència: **[enllaç a la captura]**
- *Commit* o *pull request*: **[6ab72bd](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/6ab72bd61835367dd467fff59b32ce0fe93a941d)**
- Explicació individual: **[Thiago: ...]**
- Ús d'IA, si n'hi ha hagut:

## Proves que hem de poder repetir

| Arrencada del projecte | Executar `Ra2JdbcDemo` amb la configuració per defecte | La connexió s'obre i es crea la base de dades. El programa s'atura a «RA2-ISSUE-03 pendent» | **[enllaç]** |
| Operació de modificació | Pendent (RA2-ISSUE-04, 05 i 06) | Pendent | Pendent |
| Consulta de dades | Pendent (RA2-ISSUE-07) | Pendent | Pendent |
| Cas d'error controlat | Base de dades ja creada. Executar amb `-Dcomputercenter.db.password=dolenta` | «Wrong user name or password [28000-224]». El programa mostra l'error i acaba sense excepció | **[enllaç]** |
| Operació agrupada o transacció | Pendent (RA2-ISSUE-09) | Pendent | Pendent |

## Decisions i dubtes de l'equip

| 2026-11-19 | RA2-ISSUE-02 | Cal carregar el driver d'H2 amb `Class.forName`? | 
| No cal: el driver es registra sol i `DriverManager` el troba per la URL `jdbc:h2:` |
| [6ab72bd](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/6ab72bd61835367dd467fff59b32ce0fe93a941d) |

## Ús responsable d'IA

No hem utilitzat en aquesta issue.


### RA2-ISSUE-03 · Estructura relacional

- Estat: **comprovat**
- Persona que l'ha iniciat: **Alex**
- Problema inicial: **el mètode `initSchema()` no creava cap taula. Llançava l'error «RA2-ISSUE-03 pendent» i la base de dades quedava buida.**
- Decisió aplicada: **crear l'estructura des del DAO amb `Statement` i `try-with-resources`. Fem servir `IF NOT EXISTS` perquè es pugui executar més d'una vegada sense error, i només inserim les dades inicials si la taula `products` és buida, per no duplicar productes.**
- Canvis fets: **`src/dao/ProductDaoImplJDBC.java`, mètode `initSchema()`: taules `products` i `inventory_history` (amb clau forana a `products`), àlies `STOCK_ALERT_LIMIT` i tres productes inicials.**
- Prova realitzada: **hem executat `Ra2JdbcDemo` tres vegades. Ja no surt «RA2-ISSUE-03 pendent»: ara s'atura a «RA2-ISSUE-07 pendent». Les dues taules existeixen i continua havent-hi tres productes.**
- Evidència: **[enllaç a la captura]**
- *Commit* o *pull request*: **[13fd0e2](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/13fd0e22bacaf15bab6b653fe1c9ed5566fb0e9b)**
- Explicació individual: **[Alex: ...] [Thiago: ...]**
- Ús d'IA, si n'hi ha hagut: **[completeu]**

## Proves que hem de poder repetir

| Cas que comprovem | Dades o condicions inicials | Resultat observat | Evidència |
| --- | --- | --- | --- |
| Arrencada del projecte | Executar `Ra2JdbcDemo` amb la configuració per defecte | La connexió s'obre i es creen les taules. El programa s'atura a «RA2-ISSUE-07 pendent» | **[enllaç]** |
| Operació de modificació | Pendent (RA2-ISSUE-04, 05 i 06) | Pendent | Pendent |
| Consulta de dades | Pendent (RA2-ISSUE-07) | Pendent | Pendent |
| Cas d'error controlat | Base de dades ja creada. Executar amb `-Dcomputercenter.db.password=dolenta` | «Wrong user name or password [28000-224]». El programa mostra l'error i acaba sense excepció | **[enllaç]** |
| Operació agrupada o transacció | Pendent (RA2-ISSUE-09) | Pendent | Pendent |

## Decisions i dubtes de l'equip

| Data | *Issue* | Decisió o dubte | Com s'ha resolt | Referència |
| --- | --- | --- | --- | --- |
| 2026-11-24 | RA2-ISSUE-03 | Com evitem duplicar productes si `initSchema()` s'executa més d'una vegada? | Comptem les files amb `SELECT COUNT(*)` i només inserim si la taula és buida | [13fd0e2](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/13fd0e22bacaf15bab6b653fe1c9ed5566fb0e9b) |

## Ús responsable d'IA

No hem utilitzat a aquesta issue.

### RA2-ISSUE-04 · Inserció de dades

- Estat: **comprovat**
- Persona que l'ha iniciat: **Thiago**
- Problema inicial: **el mètode `insertProduct()` no inseria cap producte. Llançava l'error «RA2-ISSUE-04 pendent» i no es podia afegir cap producte nou a la base de dades.**
- Decisió aplicada: **fer la inserció amb `PreparedStatement` i la sentència `INSERT INTO products(name, wholesaler_price, available, stock) VALUES (?, ?, ?, ?)`. Assignem cada valor amb `setString`, `setDouble`, `setBoolean` i `setInt`, així no concatenem cap valor de l'usuari dins l'SQL. Fem servir `try-with-resources` perquè el `PreparedStatement` es tanqui sol, i retornem el resultat d'`executeUpdate()`, que són les files afectades.**
- Canvis fets: **`src/dao/ProductDaoImplJDBC.java`, mètode `insertProduct()`: hem tret el TODO i el `throw pending(...)`, hem afegit la inserció parametritzada i l'import de `java.sql.PreparedStatement`.**
- Prova realitzada: **des de la finestra de l'aplicació hem afegit «GTA VI» (preu 67.00, estoc 6). Després, amb l'aplicació tancada, hem fet `SELECT * FROM products` a la consola d'H2 i surten els tres productes inicials i «GTA VI» (4 files). `Ra2JdbcDemo` continua aturant-se a «RA2-ISSUE-07 pendent», perquè comença llistant l'inventari.**
- Evidència: **[captura](evidencies/issue04.png)**
- *Commit* o *pull request*: **[2d94ca4](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/2d94ca49f92eceb7de36e5cf8d64b46ea1599d65)**
- Explicació individual: **[Alex: ...] [Thiago: ...]**
- Ús d'IA, si n'hi ha hagut: **[completeu]**

## Proves que hem de poder repetir

| Cas que comprovem | Dades o condicions inicials | Resultat observat | Evidència |
| --- | --- | --- | --- |
| Arrencada del projecte | Executar `Ra2JdbcDemo` amb la configuració per defecte | La connexió s'obre i es creen les taules. El programa s'atura a «RA2-ISSUE-07 pendent» | **[enllaç]** |
| Operació de modificació | Inserció (RA2-ISSUE-04): afegir «GTA VI» (67.00, estoc 6) des de l'aplicació. Actualització i eliminació pendents (RA2-ISSUE-05 i 06) | El producte es desa i apareix en una consulta posterior amb `SELECT * FROM products` | **[captura](evidencies/issue04.png)** |
| Consulta de dades | Pendent (RA2-ISSUE-07) | Pendent | Pendent |
| Cas d'error controlat | Base de dades ja creada. Executar amb `-Dcomputercenter.db.password=dolenta` | «Wrong user name or password [28000-224]». El programa mostra l'error i acaba sense excepció | **[enllaç]** |
| Operació agrupada o transacció | Pendent (RA2-ISSUE-09) | Pendent | Pendent |

## Decisions i dubtes de l'equip

| Data | *Issue* | Decisió o dubte | Com s'ha resolt | Referència |
| --- | --- | --- | --- | --- |
| 2026-11-26 | RA2-ISSUE-04 | Com evitem que un nom amb cometes o un valor de l'usuari trenqui la sentència o permeti injecció SQL? | Fem servir `PreparedStatement` amb `?` i assignem els valors amb `setString`, `setDouble`, `setBoolean` i `setInt` en lloc de concatenar-los | [2d94ca4](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/2d94ca49f92eceb7de36e5cf8d64b46ea1599d65) |

## Ús responsable d'IA

No hem fet us en aquest issue

### RA2-ISSUE-06 · Eliminació controlada

- Estat: **comprovat**
- Persona que l'ha iniciat: **Thiago**
- Problema inicial: **el mètode `deleteProduct()` no eliminava cap producte. Llançava l'error «RA2-ISSUE-06 pendent» i no es podia esborrar cap producte de la base de dades.**
- Decisió aplicada: **fer l'eliminació amb `PreparedStatement` i la sentència `DELETE FROM products WHERE name = ?`, assignant el nom amb `setString` per no concatenar-lo a l'SQL. Retornem el resultat d'`executeUpdate()`: 1 si el producte existia i 0 si no existia, sense llançar error. Si el producte té historial a `inventory_history`, la clau forana no deixa esborrar-lo (error 23503); en aquest cas capturem l'error i llancem un missatge que explica per què no es pot eliminar, i el producte no s'esborra.**
- Canvis fets: **`src/dao/ProductDaoImplJDBC.java`, mètode `deleteProduct()`: hem tret el TODO i el `throw pending(...)` i hem afegit l'eliminació parametritzada amb el control de l'error de clau forana.**
- Prova realitzada: **des de la finestra de l'aplicació hem escrit «SSD 1TB» al camp del nom i l'hem eliminat; l'aplicació mostra «Files eliminades: 1». Després, amb l'aplicació tancada, hem fet `SELECT * FROM products` a la consola d'H2 i «SSD 1TB» ja no hi és: queden «RAM 32GB», «Teclat mecanic» i «GTA VI» (3 files).**
- Evidència: **[captura de l'aplicació](evidencies/issue06_app.png)** · **[captura de la consulta](evidencies/issue06.png)**
- *Commit* o *pull request*: **[260b10d](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/260b10d3de462c430706158e3dfd9beaa9cd924a)**
- Explicació individual: **[Alex: ...] [Thiago: ...]**
- Ús d'IA, si n'hi ha hagut: **[completeu]**

## Proves que hem de poder repetir

| Cas que comprovem | Dades o condicions inicials | Resultat observat | Evidència |
| --- | --- | --- | --- |
| Arrencada del projecte | Executar `Ra2JdbcDemo` amb la configuració per defecte | La connexió s'obre i es creen les taules. El programa s'atura a «RA2-ISSUE-07 pendent» | **[enllaç]** |
| Operació de modificació | Inserció (RA2-ISSUE-04): afegir «GTA VI» des de l'aplicació. Eliminació (RA2-ISSUE-06): eliminar «SSD 1TB» des de l'aplicació. Actualització pendent (RA2-ISSUE-05) | «GTA VI» apareix a la consulta posterior. L'eliminació mostra «Files eliminades: 1» i «SSD 1TB» ja no surt a la consulta posterior | **[captura 04](evidencies/issue04.png)** · **[captura 06 app](evidencies/issue06_app.png)** · **[captura 06 consulta](evidencies/issue06.png)** |
| Consulta de dades | Pendent (RA2-ISSUE-07) | Pendent | Pendent |
| Cas d'error controlat | Base de dades ja creada. Executar amb `-Dcomputercenter.db.password=dolenta` | «Wrong user name or password [28000-224]». El programa mostra l'error i acaba sense excepció | **[enllaç]** |
| Operació agrupada o transacció | Pendent (RA2-ISSUE-09) | Pendent | Pendent |

## Decisions i dubtes de l'equip

| Data | *Issue* | Decisió o dubte | Com s'ha resolt | Referència |
| --- | --- | --- | --- | --- |
| 2026-11-26 | RA2-ISSUE-06 | Què passa si eliminem un producte que té historial a `inventory_history`? | La clau forana no ho permet (error 23503). Capturem aquest error i llancem un missatge que explica per què no es pot eliminar; el producte no s'esborra | [260b10d](https://github.com/ThiagoBemen3/ComputerCenterShopv1_javafx/commit/260b10d3de462c430706158e3dfd9beaa9cd924a) |

## Ús responsable d'IA

Hem utilitzat ia per la aplicacio de preparedStatement

## Proves que hem de poder repetir

| Cas que comprovem | Dades o condicions inicials | Resultat observat | Evidència |
| --- | --- | --- | --- |
| Arrencada del projecte | **[completeu]** | **[completeu]** | **[enllaç]** |
| Operació de modificació | **[completeu]** | **[completeu]** | **[enllaç]** |
| Consulta de dades | **[completeu]** | **[completeu]** | **[enllaç]** |
| Cas d'error controlat | **[completeu]** | **[completeu]** | **[enllaç]** |
| Operació agrupada o transacció | **[completeu]** | **[completeu]** | **[enllaç]** |


## Decisions i dubtes de l'equip

| Data | *Issue* | Decisió o dubte | Com s'ha resolt | Referència |
| --- | --- | --- | --- | --- |
| **[AAAA-MM-DD]** | **[RA2-ISSUE-XX]** | **[completeu]** | **[completeu]** | **[enllaç]** |

## Ús responsable d'IA

El nivell previst és **IA-1**: podeu usar eines d'IA com a suport per entendre conceptes, formular hipòtesis o revisar una explicació. No substitueixen les proves del projecte ni l'explicació individual.

Si n'heu fet ús, anoteu a l'*issue* corresponent què heu preguntat, què heu contrastat amb el projecte i quina decisió final heu pres. No enganxeu una resposta d'IA com si fos una prova de funcionament.

## Abans de donar la pràctica per preparada

- [ ] Els *issues* P0 tenen un resultat comprovat o una incidència explicada.
- [ ] El repositori conté *commits* que permeten seguir el treball de l'equip.
- [ ] Les proves de funcionament tenen evidències enllaçades.
- [ ] Les decisions sobre connector, consultes, recursos, transaccions i procediments estan explicades amb paraules pròpies.
- [ ] Tots dos integrants poden defensar individualment les decisions tècniques del repositori.
- [ ] El README no inclou solucions copiades ni contingut fora de l'abast de RA2.

---

*Aquesta plantilla és un suport per documentar el treball. El que acredita el procés és el repositori de l'equip, amb els seus canvis, proves, decisions i explicacions.*
