# An Teanga Ríomhchláraithe Rust

[An Teanga Ríomhchláraithe Rust](title-page.md)
[Réamhfhocal](foreword.md)
[Réamhrá](ch00-00-introduction.md)

## Tús a chur leis

- [Tús a chur leis](ch01-00-getting-started.md)

  - [Suiteáil](ch01-01-installation.md)
  - [Dia duit, a Dhomhanda!](ch01-02-hello-world.md)
  - [Dia duit, Cargo!](ch01-03-hello-cargo.md)

- [Cluiche tomhas á ríomhchlárú](ch02-00-guessing-game-tutorial.md)

- [Coincheapa Coitianta Cláir](ch03-00-common-programming-concepts.md)

  - [Athróga agus Inathraitheacht](ch03-01-variables-and-mutability.md)
  - [Cineál Sonraí](ch03-02-data-types.md)
  - [Feidhmeanna](ch03-03-how-functions-work.md)
  - [Tuairimí](ch03-04-comments.md)
  - [Sreabhadh Rialaithe](ch03-05-control-flow.md)

- [Úinéireacht a Thuiscint](ch04-00-understanding-ownership.md)

  - [Cad is Úinéireacht ann?](ch04-01-what-is-ownership.md)
  - [Tagairtí agus Iasachtaí](ch04-02-references-and-borrowing.md)
  - [An Cineál Slice](ch04-03-slices.md)

- [Structs a Úsáid chun Sonraí Gaolmhara a Struchtúrú](ch05-00-structs.md)

  - [Structs a shainiú agus a thionscnamh](ch05-01-defining-structs.md)
  - [Clár Samplach ag Úsáid Structs](ch05-02-example-structs.md)
  - [Modh Comhréir](ch05-03-method-syntax.md)

- [Áirimh agus Meaitseáil Patrún](ch06-00-enums.md)
  - [Áirimh a shainiú](ch06-01-defining-an-enum.md)
  - [An Tógáil Sreabhadh Rialaithe `match`](ch06-02-match.md)
  - [Sreabhadh Rialaithe Gonta le `if let` agus `let else`](ch06-03-if-let.md)

## Litearthacht Bunúsach Rust

- [Tionscadail atá ag Fás a Bhainistiú le Pacáistí, cliathbhoscaí agus Modúil](ch07-00-managing-growing-projects-with-packages-crates-and-modules.md)

  - [Pacáistí agus cliathbhoscaí](ch07-01-packages-and-crates.md)
  - [Modúil a Shainmhíniú chun Scóip agus Príobháideacht a Rialú](ch07-02-defining-modules-to-control-scope-and-privacy.md)
  - [Cosáin chun Tagairt a Dhéanamh do Mhír i gCrann an Mhodúil](ch07-03-paths-for-referring-to-an-item-in-the-module-tree.md)
  - [Cosáin a Thabhairt isteach sa Scóip leis an Eochairfhocal `use`](ch07-04-bringing-paths-into-scope-with-the-use-keyword.md)
  - [Modúil a Scaradh ina gComhaid Éagsúla](ch07-05-separating-modules-into-different-files.md)

- [Bailiúcháin Choitianta](ch08-00-common-collections.md)

  - [Liostaí Luachanna a Stóráil le Veicteoirí](ch08-01-vectors.md)
  - [Téacs Ionchódaithe UTF-8 a Stóráil le Teaghráin](ch08-02-strings.md)
  - [Eochracha le Luachanna Gaolmhara a Stóráil i Léarscáileanna Hash](ch08-03-hash-maps.md)

- [Láimhseáil Earráide](ch09-00-error-handling.md)

  - [Earráidí do-aisghabhála le `panic!`](ch09-01-unrecoverable-errors-with-panic.md)
  - [Earráidí Inghnóthaithe le `Result`](ch09-02-recoverable-errors-with-result.md)
  - [Chun `panic!` nó Gan `panic!`](ch09-03-to-panic-or-not-to-panic.md)

- [Cineálacha Cineálacha, Tréithe, agus Saoil](ch10-00-generics.md)

  - [Cineálacha Sonraí Ginearálta](ch10-01-syntax.md)
  - [Tréithe: Iompar Comhroinnte a Shainmhíniú](ch10-02-traits.md)
  - [Tagairtí a Bhailíochtú le Saoil](ch10-03-lifetime-syntax.md)

- [Trialacha Uathoibrithe a Scríobh](ch11-00-testing.md)

  - [Conas a Scríobh Tástálacha](ch11-01-writing-tests.md)
  - [Conas a Reáchtáiltear Tástálacha a Rialú](ch11-02-running-tests.md)
  - [Eagraíocht Tástála](ch11-03-test-organization.md)

- [Tionscadal I/O: Clár Líne Ceannais a Thógáil](ch12-00-an-io-project.md)
  - [Ag glacadh le Argóintí Líne Ordú](ch12-01-accepting-command-line-arguments.md)
  - [Comhad a Léamh](ch12-02-reading-a-file.md)
  - [Athfhachtóiriú chun Modúlacht agus Láimhseáil Earráidí a Fheabhsú](ch12-03-improving-error-handling-and-modularity.md)
  - [Feidhmiúlacht na Leabharlainne a Fhorbairt le Forbairt Thrialacha](ch12-04-testing-the-librarys-functionality.md)
  - [Ag obair le hAthróga Comhshaoil](ch12-05-working-with-environment-variables.md)
  - [Teachtaireachtaí Earráide a Scríobh go Earráid Chaighdeánach In ionad Aschur Caighdeánach](ch12-06-writing-to-stderr-instead-of-stdout.md)

## Ag smaoineamh i Rust

- [Gnéithe Feidhmiúla Teanga: Iterators and Closures](ch13-00-functional-features.md)

  - [Dúnadh: Feidhmeanna Gan Ainm a Ghabhann A dTimpeallacht](ch13-01-closures.md)
  - [Sraith Míreanna a Phróiseáil le Iterators](ch13-02-iterators.md)
  - [Ár dTionscadal I/O a Fheabhsú](ch13-03-improving-our-io-project.md)
  - [Feidhmíocht a Chomparáid: Lúba vs. Atrialltóirí](ch13-04-performance.md)

- [Tuilleadh faoi Cargo agus Crates.io](ch14-00-more-about-cargo.md)

  - [Tógálacha a shaincheapadh le Próifílí Eisiúna](ch14-01-release-profiles.md)
  - [Cearrbhachas a Crate go Crates.io](ch14-02-publishing-to-crates-io.md)
  - [Spásanna Cargo](ch14-03-cargo-workspaces.md)
  - [Binaries a shuiteáil ó Crates.io le `cargo install`](ch14-04-installing-binaries.md)
  - [Lasta a Shíneadh le Orduithe Saincheaptha](ch14-05-extending-cargo.md)

- [Pointeoirí Cliste](ch15-00-smart-pointers.md)

  - [Bain úsáid as `Bosca<T>` chun Pointe ar Shonraí ar an Charn](ch15-01-box.md)
  - [Ag Caitheamh le Pointeoirí Cliste Cosúil le Tagairtí Rialta leis an dTréith `Deref`](ch15-02-deref.md)
  - [Cód Rith ar Ghlantachán leis an Trait `Drop`](ch15-03-drop.md)
  - [`Rc<T>`, an Pointeoir Cliste a Chomhairtear le Tagairt](ch15-04-rc.md)
  - [`RefCell<T>` agus an Patrún Inmheánach Mutability](ch15-05-interior-mutability.md)
  - [Is féidir le Timthriallta Tagartha Cuimhne a sceitheadh](ch15-06-reference-cycles.md)

- [Comhthráthacht Gan Eagla](ch16-00-concurrency.md)
    - [Úsáid Snáitheanna chun Cód a Rith ag an am céanna](ch16-01-threads.md)
    - [Ag Bain úsáid as Teachtaireacht chun Sonraí a Aistriú Idir Snáitheanna](ch16-02-message-passing.md)
    - [Comhairgeadra Comh-Stáit](ch16-03-shared-state.md)
    - [Comhairgeadra Leathnaithe leis na Tréithe `Sync` agus `Send`](ch16-04-extensible-concurrency-sync-and-send.md)

- [Bunúsacha na Clársceidealaithe Asincrónaí: Asincrónach, Fanacht, Todhchaí, agus Sruthanna](ch17-00-async-await.md)
    - [Futures agus an Comhréir Async](ch17-01-futures-and-syntax.md)
    - [Comhairgeadra Le Async](ch17-02-concurrency-with-async.md)
    - [Ag Obair Le hAon Líon Todhchaíochtaí](ch17-03-more-futures.md)
    - [Sruthanna](ch17-04-streams.md)
    - [Tochailt ar na Tréithe le haghaidh Async](ch17-05-traits-for-async.md)
    - [Todhchaí, Tascanna, agus Snáitheanna](ch17-06-futures-tasks-threads.md)

- [Gnéithe Ríomhchláraithe atá Dírithe ar Réada de Rust](ch18-00-oop.md)
    - [Saintréithe na dTeangacha atá Dírithe ar Oibiachtaí](ch18-01-what-is-oo.md)
    - [Ag Úsáid Cuspóirí Tréith a Ligeann Luachanna de Chineálacha Éagsúla](ch18-02-trait-objects.md)
    - [Patrún Dearaidh atá Dírithe ar Oibiachtaí a Chur i bhFeidhm](ch18-03-oo-design-patterns.md)

## Ardábhair

- [Pátrúin agus Meaitseáil](ch19-00-patterns.md)
    - [Is féidir na Pátrúin Áiteanna Uile a Úsáid](ch19-01-all-the-places-for-patterns.md)
    - [Refutability: Cé acu an bhféadfadh go dteipfeadh ar phatrún a mheaitseáil](ch19-02-refutability.md)
    - [Comhréir Phatrúin](ch19-03-pattern-syntax.md)

- [Ardghnéithe](ch20-00-advanced-features.md)
    - [Rust neamhshábháilte](ch20-01-unsafe-rust.md)
    - [Ardtréithe](ch20-03-advanced-traits.md)
    - [Ardchineálacha](ch20-04-advanced-types.md)
    - [Ardfheidhmeanna agus Dúnadh](ch20-05-advanced-functions-and-closures.md)
    - [Macraí](ch20-06-macros.md)

- [Tionscadal Deiridh: Freastalaí Gréasáin Ilsnáithe a Thógáil](ch21-00-final-project-a-web-server.md)
    - [Freastalaí Gréasáin Snáithe Aonair a Thógáil](ch21-01-single-threaded.md)
    - [Ár bhFreastalaí Snáithe Aonair a iompú ina Fhreastalaí Ilsnáithe](ch21-02-multithreaded.md)
    - [Múchadh agus Glanta Grásta](ch21-03-graceful-shutdown-and-cleanup.md)

- [Aguisín](appendix-00.md)
    - [A - Eochairfhocail](appendix-01-keywords.md)
    - [B - Oibreoirí agus Siombailí](appendix-02-operators.md)
    - [C - Tréithe In-Díorthaithe](appendix-03-derivable-traits.md)
    - [D - Uirlisí Úsáideacha Forbartha](appendix-04-useful-development-tools.md)
    - [E - Eagráin](appendix-05-editions.md)
    - [F - Aistriúcháin na Leabhar](appendix-06-translation.md)
    - [G - Conas a Dhéantar Rust agus “Rust na hOíche”](appendix-07-nightly-rust.md)
