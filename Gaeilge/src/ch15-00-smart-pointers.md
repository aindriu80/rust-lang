# Leideanna Cliste

Is coincheap ginearálta é _pointeoir_ d’athróg ina bhfuil seoladh i
cuimhne. Tagraíonn an seoladh seo do, nó “pointí ag,” do roinnt sonraí eile. An chuid is mó
Is tagairt í an cineál pointeoir coitianta i Rust, ar fhoghlaim tú faoi i
Caibidil 4. Cuirtear tagairtí in iúl leis an tsiombail `&` agus faigheann siad an luach ar iasacht
pointe ar. Níl aon chumais speisialta acu seachas tagairt a dhéanamh dóibh
sonraí, agus gan aon forchostais.

Ar an láimh eile, is struchtúir sonraí iad _Smart pointers_ a fheidhmíonn mar a
pointeoir ach tá meiteashonraí agus cumais bhreise acu freisin. Coincheap na
níl leideanna cliste uathúil do Rust: tháinig leideanna cliste ó C ++ agus tá siad ann
i dteangacha eile chomh maith. Tá éagsúlacht leideanna cliste sainithe ag Rust sa
leabharlann caighdeánach a sholáthraíonn feidhmiúlacht thar an gceann a sholáthraíonn tagairtí.
Chun an coincheap ginearálta a iniúchadh, féachfaimid ar chúpla sampla éagsúla de
leideanna cliste, lena n-áirítear cineál pointeoir cliste _reference counting_. seo
cuireann pointeoir ar do chumas sonraí úinéirí iolracha a bheith agat trí súil a choinneáil orthu
líon na n-úinéirí agus, nuair nach bhfuil aon úinéirí fágtha, na sonraí a ghlanadh.

Tá difríocht bhreise ag meirge, lena choincheap úinéireachta agus iasachtaíochta
idir thagairtí agus leideanna cliste: cé nach bhfaigheann tagairtí ach sonraí ar iasacht, i
go leor cásanna, leideanna cliste _ow_ na sonraí a díríonn siad ar.

Cé nár thugamar glaoch orthu mar sin ag an am, thángamar ar roinnt acu cheana féin
leideanna cliste sa leabhar seo, ina measc `String` agus `Vec<T>` i gCaibidil 8. An dá cheann
áirítear na cineálacha seo mar threoracha cliste mar go bhfuil roinnt cuimhne acu agus go gceadaíonn siad duit
a ionramháil. Tá meiteashonraí agus cumais nó ráthaíochtaí breise acu freisin.
Stringeann `String`, mar shampla, a chumas mar mheiteashonraí agus tá an breiseán breise aige
an cumas a áirithiú go mbeidh a chuid sonraí bailí i gcónaí UTF-8.

De ghnáth cuirtear leideanna cliste i bhfeidhm ag baint úsáide as struchtúir. Murab ionann agus gnáth
struct, leideanna cliste a chur i bhfeidhm na tréithe `Deref` agus `Drop`. An `Deref`
Ceadaíonn an trait do shampla den struchtúr pointeoir cliste é féin a iompar mar thagairt
ionas gur féidir leat do chód a scríobh chun oibriú le tagairtí nó le leideanna cliste.
Ligeann an tréith `Drop` duit an cód a rithtear nuair a bhíonn tú a shaincheapadh
Téann an pointeoir cliste as an raon feidhme. Sa chaibidil seo, pléifimid an dá cheann
tréithe agus a léiriú cén fáth a bhfuil siad tábhachtach do leideanna cliste.

Ós rud é gur patrún dearadh ginearálta é an patrún pointeoir cliste a úsáidtear
go minic i Rust, ní chlúdóidh an chaibidil seo gach pointeoir cliste atá ann cheana féin. go leor
tá a gcuid leideanna cliste féin ag leabharlanna, agus is féidir leat do chuid féin a scríobh fiú. Déanfaimid
clúdaíonn siad na leideanna cliste is coitianta sa ghnáthleabharlann:

- `Bosca <T>` chun luachanna a leithdháileadh ar an gcarn
- `Rc<T>`, cineál comhairimh tagartha a chumasaíonn úinéireacht iolrach
- `Ref<T>` agus `RefMut<T>`, a rochtain trí `RefCell<T>`, cineál a fhorfheidhmíonn
 na rialacha iasachtaithe ag am rite in ionad am tiomsaithe

Ina theannta sin, clúdóimid an patrún _interior mutability_ nuair nach féidir é a mhalartú
Nochtann cineál API chun luach istigh a shóchán. Déanfaimid plé freisin
_reference cycles_: conas is féidir leo cuimhne a sceitheadh ​​agus conas iad a chosc.

Léimís isteach!