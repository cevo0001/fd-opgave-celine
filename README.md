REFLEKTION:

I dette projekt har jeg arbejdet med at strukturere mit website i Astro-komponenter, så hver sektion (f.eks. hero, services, projections, core values, newsletter osv.) er adskilt i sin egen fil. Det har gjort koden mere overskuelig og nemmere at vedligeholde.

En af de største udfordringer var at få de forskellige sektioner til at fungere responsivt, især fordi projektet var kodet desktop-first. Her arbejdede jeg med media queries og procent-baserede enheder for at sikre, at layoutet skalerer korrekt på mobil. Det har vi lært fra day one, at man altid skal kode mobile-first, så det var en kæmpe ups'er fra min side af. Derudover har jeg været tidspresset, og været ret bagud fra start, så det har været en stor opgave at håndterer, derfor også valget af at nå at fokuserer på en side og gøre den ordentligt, så forside, og login knappen virker.

En stor succes var at få JavaScript-delen i Financial Projections-komponenten til at fungere, så kortene kan skifte aktiv tilstand, når man klikker på pilene. Det viser brug af interaktivitet i et ellers statisk layout.

Jeg har også implementeret en login-popup, som åbnes og lukkes via addEventListener i JavaScript – en funktion der viser samspillet mellem HTML, CSS og JS på en simpel og effektiv måde.

Jeg har især brugt CSS Grid til at skabe jævne layouts med flere kolonner, f.eks. i core-values-sektionen:
.cv-grid {
display: grid;
grid-template-columns: repeat(4, 1fr);
gap: 1.5rem;
}

og Flexbox i områder, hvor der kræves fleksibel justering og centrering af indhold – som i hero og newsletter-komponenterne. Jeg har også gjort brug af moderne CSS som :has()-selektoren, som gør det muligt at style forældre baseret på indholdet, hvilket giver en mere vedligeholdelsesvenlig og fremtidssikker struktur.

Derudover har jeg integreret JavaScript-interaktivitet, bl.a. i Financial Projections-komponenten, hvor kortene skifter aktiv tilstand, når man klikker på pilene:
nextBtn.addEventListener("click", () => {
activeIndex = (activeIndex + 1) % cards.length;
updateCards();
});

og i den enkle login-popup, hvor jeg bruger addEventListener og classList.add/remove til at åbne og lukke et overlay – en løsning der viser samspillet mellem HTML, CSS og JS.

Min CSS er organiseret i to niveauer:

Global styling i global.css, hvor jeg har defineret farve- og typografivariable som:
:root {
--gul: #ffcc4a;
--grøn: #4eaf4e;
--sort: #181818;
--grå: #f5f5f5;
--hvid: #ffffff;
}
samt import af Google-fonten Cabin, som bruges på hele sitet.

Komponent-specifik styling i hver .astro-fil under @layer components, så hver sektion har sin egen afgrænsede styling uden at påvirke de andre dele af siden.

Denne struktur har gjort projektet både overskueligt, responsivt og let at vedligeholde, samtidig med at det viser brugen af centrale frontend-principper som grid, flex, :has(), og JavaScript-interaktivitet i praksis.

# Opgaveskabelon til Frontend Design tema på Frontend-valgfaget

Se opgavebeskrivelsen på Fronter.

## Medfølgende Data

Der medfølger indholdsdata i form af lokale JSON-filer, som du kan bruge til din opgave. Det er ikke et krav til opgaven, men det kan gøre det nemmere og hurtigere at få tekst og billeder ind i dit projekt.

Bemærk, at CaseStudy-siden allerede inkluderer data fra en lokal JSON-fil.

Dokumentationen til anvendelsen af dataene finder du på: [https://frontend-design-theme.netlify.app/](https://frontend-design-theme.netlify.app/).

Her er et eksempel på, hvordan du kan bruge dataene i dine Astro-komponenter:

```astro
import employees from "@data/employees.json"; console.log(employees);
```

## Brug af hjælpekomponenter

### DynamicImage.astro

Brug denne komponent til at vise billeder dynamisk fra lokale datafiler. Du skal blot sende stien fra datasættet direkte til komponenten.

Eksempel med data:

```astro
{
  employees.map((employee) => (
    <DynamicImage
      imagePath={employee.img}
      altText={employee.name}
      width={200}
      height={200}
    />
  ))
}
```

### DynamicIcon.astro

`DynamicIcon` bruges til at vise SVG-ikoner dynamisk baseret på et navn fra dine data.

Eksempel med data:

```astro
{employee.social_links.map((link) => <DynamicIcon name={link.icon} />)}
```

Her vises et ikon for hvert socialt medie, hvor `icon`-feltet matcher filnavnet på SVG-ikonet i `src/icons/`.

### HeroBgWrapper.astro

HeroBgWrapper bruges til Hero-sektioner på diverse undersider. Brug `imagePath` til at angive baggrundsbilledet. Du skal selv hente billederne fra Figma og lægge dem i mappen `src/assets/images`. Henvis derefter kun til filnavnet (f.eks. 'case.webp').

Alt markup du placerer mellem <HeroBgWrapper> og </HeroBgWrapper> bliver vist ovenpå baggrunden.

Eksempel:

```astro
<HeroBgWrapper imagePath="case.webp" class="hero-bg">
  <h1>Din overskrift</h1>
</HeroBgWrapper>
```

Du kan tilføje ekstra styling via `class` eller `style`-props, og alt indhold mellem tags bliver vist ovenpå baggrunden.

---

## Import af SVG-ikoner direkte

Du kan også importere SVG-ikoner direkte i dine komponenter, hvis du ønsker mere kontrol eller styling:

```astro
import Checkmark from "@icons/checkmark.svg";

<Checkmark width={32} height={32} class="my-icon" />
```

Se evt. `src/pages/svgs.astro` for flere eksempler på direkte import og brug af SVG-ikoner.
