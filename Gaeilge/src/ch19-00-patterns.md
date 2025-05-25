# Patrúin agus Meaitseáil

Is comhréir speisialta i Rust iad _Patrúin_ le haghaidh meaitseáil i gcoinne struchtúr
cineálacha, casta agus simplí araon. Trí phatrúin a úsáid i gcomhar le habairtí `match`
agus coincheapa eile, tugtar níos mó smachta duit ar shreabhadh rialaithe
cláir. Is éard atá i bpatrún meascán éigin de na nithe seo a leanas:

- Litreacha
- Eagair, enums, struchtúir, nó tuples dístruchtúrtha
- Athróga
- Cártaí Fiáine
- Sealbhóirí Áit

I measc roinnt patrún samplach tá `x`, `(a, 3)`, agus `Some(Color::Red)`. Sna
comhthéacsanna ina bhfuil patrúin bailí, déanann na comhpháirteanna seo cur síos ar chruth na
sonraí. Ansin, déanann ár gclár luachanna a mheaitseáil i gcoinne na bpatrún chun a chinneadh an
bhfuil an cruth ceart sonraí aige chun leanúint ar aghaidh ag rith píosa áirithe cóid.

Chun patrún a úsáid, déanaimid comparáid idir é agus luach éigin. Má mheaitseálann an patrún an
luach, úsáidimid na codanna luacha inár gcód. Cuimhnigh ar na habairtí `match` i
gCaibidil 6 a d'úsáid patrúin, amhail an sampla den mheaisín sórtála mona. Má
oireann an luach do chruth an phatrúin, is féidir linn na píosaí ainmnithe a úsáid. Mura
n-oireann, ní rithfidh an cód a bhaineann leis an bpatrún.

Is tagairt í an chaibidil seo do gach rud a bhaineann le patrúin. Clúdóimid na
áiteanna bailí chun patrúin a úsáid, an difríocht idir patrúin inchéillithe agus neamh-inchéillithe,
agus na cineálacha éagsúla comhréir patrún a d'fhéadfá a fheiceáil. Faoi
dheireadh na caibidle, beidh a fhios agat conas patrúin a úsáid chun go leor coincheapa a chur in iúl ar
bhealach soiléir.