# Tionscadail atá ag Fás a Bhainistiú le Pacáistí, cliathbhoscaí agus Modúil

De réir mar a scríobhann tú cláir mhóra, tiocfaidh eagrú do chód níos mó agus níos mó
tábhachtach. Trí fheidhmiúlacht ghaolmhar a ghrúpáil agus cód a scaradh le chéile
gnéithe, soiléireoidh tú cá háit a bhfaighidh tú cód a chuireann ceann ar leith i bhfeidhm
gné agus cá háit le dul chun an chaoi a n-oibríonn gné a athrú.

Tá na cláir atá scríofa againn go dtí seo in aon mhodúl amháin i gcomhad amháin. Mar a
Fásann an tionscadal, ba cheart duit cód a eagrú trína roinnt ina il-mhodúil
agus ansin comhaid iolracha. Is féidir le cliathbhoscaí dénártha iolracha agus
go roghnach cliathbhosca leabharlainne amháin. De réir mar a fhásann pacáiste, is féidir leat páirteanna a bhaint astu
cliathbhoscaí ar leith a thagann chun bheith ina spleáchais sheachtracha. Clúdaíonn an chaibidil seo gach
na teicníochtaí seo. I gcás tionscadal an-mhór a chuimsíonn sraith de idirghaolmhar
pacáistí a fhorbraíonn le chéile, soláthraíonn lasta _spásanna oibre_, a chlúdóimid
sa [“Lasta Workspaces”][workspaces]<!-- neamhaird --> i gCaibidil 14.

Déanfaimid plé freisin ar shonraí cur chun feidhme a chuimsiú, a ligeann duit athúsáid
cód ag leibhéal níos airde: nuair a bheidh oibríocht curtha i bhfeidhm agat, is féidir le cód eile
glaoch ar do chód trína chomhéadan poiblí gan a bheith ar an eolas conas an
oibreacha forfheidhmithe. Sainmhíníonn an bealach a scríobhann tú cód cé na codanna atá poiblí
cód eile atá le húsáid agus cé na codanna atá ina sonraí forfheidhmithe príobháideacha atá agat
an ceart chun athrú a choimeád. Is bealach eile é seo chun teorainn a chur leis an méid sonraí
caithfidh tú a choinneáil i do cheann.

Tá raon feidhme ag coincheap gaolmhar: tá a
sraith ainmneacha a shainmhínítear mar “i raon feidhme.” Nuair a bhíonn léamh, scríobh, agus
cód a thiomsú, ríomhchláraitheoirí agus tiomsaitheoirí gá go mbeadh a fhios cé acu ar leith
tagraíonn ainm ag spota ar leith d'athróg, d'fheidhm, do struchtúr, d'enum, do mhodúl,
tairiseach, nó mír eile agus cad a chiallaíonn an mhír sin. Is féidir leat scopes a chruthú agus
athrú ar na hainmneacha atá laistigh nó lasmuigh den scóip. Ní féidir dhá mhír a bheith agat leis an
ainm céanna sa raon feidhme céanna; tá uirlisí ar fáil chun coinbhleachtaí ainmneacha a réiteach.

Tá roinnt gnéithe ag Rust a ligeann duit do chóid a bhainistiú
eagraíocht, lena n-áirítear na sonraí atá nochtaithe, cé na sonraí atá príobháideach,
agus cad iad na hainmneacha atá i ngach raon feidhme i do chláir. Na gnéithe seo, uaireanta
le chéile dá ngairtear an _module system_, áirítear:

- **Pacáistí:** Gné lasta a ligeann duit cliathbhoscaí a thógáil, a thástáil agus a roinnt
- **Cliathbhosca:** Crann modúl a tháirgeann leabharlann nó inrite
- **Modúil** agus **úsáid:** Ligeann tú smacht ar an eagraíocht, ar an raon feidhme agus ar an
 príobháideacht cosáin
- **Cosáin:** Bealach chun mír a ainmniú, mar struchtúr, feidhm nó modúl

Sa chaibidil seo, clúdóidh muid na gnéithe seo go léir, pléifimid conas a idirghníomhaíonn siad, agus
mínigh conas iad a úsáid chun scóip a bhainistiú. Faoi dheireadh, ba chóir go mbeadh soladach agat
tuiscint ar chóras na modúl agus a bheith in ann oibriú le scopes cosúil le pro!

[workspaces]: ch14-03-cargo-workspaces.html