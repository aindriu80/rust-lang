# Tionscadal I/O: Clár Líne Ceannais a Thógáil

Achoimre is ea an chaibidil seo ar an iliomad scileanna atá foghlamtha agat go dtí seo agus
iniúchadh ar roinnt gnéithe caighdeánacha leabharlainne. Tógfaimid líne ordaithe
uirlis a idirghníomhaíonn le hionchur/aschur comhaid agus orduithe chun cuid de
na coincheapa Rust atá agat anois faoi do chrios.

Déanann luas, sábháilteacht meirge, aschur dénártha aonair, agus tacaíocht tras-ardáin é
teanga iontach chun uirlisí líne ceannais a chruthú, mar sin dár dtionscadal, déanfaimid
ár leagan féin a dhéanamh den uirlis chuardaigh na n-orduithe clasaiceach `grep`
(**g** cuardaigh léiriú **r**egular**e** agus **p**rint). Sna
cás úsáide is simplí, cuardaigh `grep` comhad sonraithe le haghaidh teaghrán sonraithe. Chuig
é sin a dhéanamh, glacann `grep` cosán comhaid agus teaghrán mar chuid argóintí. Ansin léann sé
an comhad, aimsíonn sé línte sa chomhad sin ina bhfuil an argóint teaghrán, agus priontaí
na línte sin.

Ar an mbealach seo, taispeánfaimid conas ár n-uirlis líne ordaithe a bhaint as an teirminéal
gnéithe a úsáideann go leor uirlisí líne ordaithe eile. Léifidh muid luach an
athróg timpeallachta chun ligean don úsáideoir iompar ár n-uirlis a chumrú.
Déanfaimid teachtaireachtaí earráide a phriontáil freisin chuig an sruth caighdeánach consól earráide (`stderr`)
in ionad aschur caighdeánach (`stdout`) ionas gur féidir leis an úsáideoir, mar shampla
aschur rathúil a atreorú chuig comhad agus teachtaireachtaí earráide fós le feiceáil ar an scáileán.

Tá ball amháin de phobal Rust, Andrew Gallant, tar éis ball iomlán a chruthú cheana féin
le feiceáil, leagan an-tapa de `grep`, ar a dtugtar `ripgrep`. Mar chomparáid, ár
Beidh leagan simplí go leor, ach beidh an chaibidil seo a thabhairt duit ar roinnt de na
eolas cúlra a theastaíonn uait chun tuiscint a fháil ar thionscadal fíordhomhain ar nós
`ripgrep`.

Cuirfidh ár dtionscadal `grep` le chéile roinnt coincheap a d'fhoghlaim tú go dtí seo:

- Cód eagraithe ([Caibidil 7][ch7]<!-- neamhaird -->)
- Ag baint úsáide as veicteoirí agus teaghráin ([Caibidil 8][ch8] <!-- neamhaird -->)
- Earráidí a láimhseáil ([Caibidil 9][ch9]<!-- neamhaird -->)
- Ag baint úsáide as tréithe agus saolréanna nuair is cuí ([Caibidil 10][ch10]<!-- neamhaird -->)
- Trialacha scríofa ([Caibidil 11][ch11]<!-- neamhaird -->)

Tabharfaimid isteach go hachomair freisin dúnta, iterators, agus réada trait, a
[Caibidil 13][ch13]<!-- neamhaird --> agus [Caibidil 18][ch18] <!-- neamhaird -->
clúdach go mion.

[ch7]: ch07-00-managing-growing-projects-with-packages-crates-and-modules.html
[ch8]: ch08-00-common-collections.html
[ch9]: ch09-00-error-handling.html
[ch10]: ch10-00-generics.html
[ch11]: ch11-00-testing.html
[ch13]: ch13-00-functional-features.html
[ch18]: ch18-00-oop.html