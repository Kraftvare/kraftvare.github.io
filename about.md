# Om Kraftvare

**Prototypen** av Kraftvare er utvikla av Vegard Gillestad for [Frammarsvik Kraft](https://no.wikipedia.org/wiki/Frammarsvik_kraftverk). Hensikten er å kunne gi best mogeleg innsikt i kraftproduksjonen. I appen kan du sjå:
- Produksjonsdata (kWt og kr). I sanntid og historikk.
- Strømpris. Dagens, morgondagen og historisk.
- Vasstand (minstevassføring). I sanntid og historikk.

## Produksjonsdata
Historik produksjon er henta frå [Elhub](https://elhub.no/om-elhub/elhub-for-sluttbruker/min-side/). Produksjon er ikkje tilgjengeleg i Elhub før dagen er over. Ein kan òg hente produksjonsdata direkte frå strømmålaren i kraftstasjonen. Når ein koblar direkte til strømmålaren vil ein kunne hente produksjon i sanntid. 

Strømmålaren i kraftstasjonen er montert på sterkstrømssida. Strømmålaren er av typen [Cewe Prometer 100](https://www.securemeters.com/product/grid-metering/prometer-100/). Ein kan koble seg til strømmålarar av denne typen ved å bruke ein [optisk probe](https://www.german-metering.com/optical-probe-products.html).
Sjølve montasjen av proben i strømålaren er veldig enkel. Den festar seg med magnet på strømmmålaren. Men sidan det kun er netteigar og autorisert personell som har tilgang til sterkstrømsida, må ein ha montør (Eviny) på plass. Deretter må ein strekkje kabelen frå proben over til svakstrømsida (For å få tilstrekkeleg lengde på kabelen kan ein måtte bruke ein [USB-forlengar](https://www.kjell.com//no/produkter/kabler-og-kontakter/usb-kabler/aktiv-usb-forlengelseskabel-10-meter-p98603?gclid=Cj0KCQiAutyfBhCMARIsAMgcRJQNaHx-vkfCJLV6HLv-_xgW1Ijq4AGMfGYlJZGU05ndIXz15hom-mMaAnNkEALw_wcB&gclsrc=aw.ds).). USB-enden av proben koblar ein inn i ein PC ([Rasberry PI](https://www.raspberrypi.com/)) på svakstrømsida.

*Det kan være verdt å nemne at Cewe Prometer 100 ikkje har ein HAN-port slik alle strømmålarar i norske privatheimar skal ha. Ein kan dermen ikkje bruke for eksempel ein norsk Tibber Pulse.*

## Minstevassføring
Vasstanden blir registert av ein [PLS](https://no.wikipedia.org/wiki/Programmerbar_logisk_styring) i kraftstasjonen. Den er montert av Geir Brattheim i [Kraftkontroll](https://kraftkontroll.no/). Verdiane blir lagra på eit minnekort. Verdiane kan hentast ut ved å koble seg til systemet via [FTP](https://en.wikipedia.org/wiki/File_Transfer_Protocol). Samme PC (Rasberry PI), nevnt over, blir brukt til å hente ut verdiar kvart kvarter.

## Strømpris
Kraftstasjonen ligg i same prisområde som huset til undertegna. Underteikna er [Tibber](https://tibber.com/no) kunde, og Tibber tilbyr eit [API](https://developer.tibber.com/) for å hente ut prisinformasjon. Prisane blir henta dagleg kl. 13.

## Komponentar i Kraftvare
- Appen. Ein kan laste ned appen via [Google Play](https://play.google.com/store/apps/details?id=no.kraftvare.android), [App Store](https://apps.apple.com/no/app/kraftvare/id1671360193?itsct=apps_box_link&itscg=30200), eller ein kan bruke appen i ein [nettlesar](https://app.kraftvare.no).
- Skya. Sentralen i systemet. All data blir lagra i skya. Appen aksesserer skya for å hente ut, og vise data.
- Noden. Nevnte PC/Raspberry PI som står i kraftstasjonen. Hentar ut data frå målar og Kraftkontroll og sender det opp i skya. 