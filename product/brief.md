# Product brief: Petsify

*Written 2026-09-19. Built from decisions already recorded in our workspace (MVP status, personas, pricing and competitor research), not from scratch.*

## 1. Problem

Three sides of the same market in Poland use separate, poor tools:

- **Breeders** get a flood of random inquiries through Facebook, Instagram and classifieds. They answer the same questions about pedigree and vaccinations by hand, and have no data on which listings actually work.
- **People adopting** have to check several shelters, foundations and adoption groups separately. Listings are out of date (the animal is already adopted) and every source uses a different format.
- **People buying a purebred pet** have no easy way to tell a responsible breeder from a puppy mill. Every listing looks different and there's no comparable format for documents or pedigree.

Today this runs on Facebook, classifieds, Google, phone calls and spreadsheets: no single place, no freshness signal, no standard format.

## 2. Who we build for

Three primary personas, chosen from the eight in our persona database (jobs to be done, main pain, trust barrier and current alternative for each). **Names, ages and quotes are illustrative, not real interviewees:** they give each persona a face so product and GTM decisions are easier to discuss. In our persona database the breeder persona is marked "researching: needs direct conversations with breeders".

- **Ewa, 43, Kraków: breeder (target paying customer).** Runs a small cattery next to a full-time job. Pain: *"I get 15 messages and 3 are from people who actually know what they're asking about."* Our hypothesis: she would pay for saved time and better leads, not for visibility alone.
- **Marta, 29, Wrocław: adopter.** Looking for a dog that fits her flat. Pain: *"I write about a dog that someone adopted three weeks ago."* She doesn't pay; her value is traffic and trust in the brand.
- **Tomasz, 34, Poznań: buyer from a breeder.** Buying a puppy for his family. Pain: *"I don't know how to check whether this breeder is just in it for the money."* The quality of his inquiry is what Ewa is really paying for.

## 3. Value proposition

**Petsify helps breeders get better inquiries and spend less time handling them, by combining a standardised profile, a qualifying questionnaire and listing performance stats in one place. On Facebook or classifieds every inquiry has to be handled by hand, with no context and no filtering.**

This follows our breeder-first positioning ([decision 0001](../decisions/0001-breeder-first.md)): breeders are our first target paying segment, and we are testing whether they will pay. Adopters and buyers create value for breeders as the demand side; they are not a paid segment today.

## 4. MVP scope

Most of the MVP already existed when this was written; the point was to name what matters and what's missing.

1. **Organization profiles (breeder, shelter, foundation) and listings.** No supply without them. *Built.*
2. **Search and filters with optional structured data** (temperament, kids, health). A concrete edge over general classifieds. *Built.*
3. **Fast contact without a forced account.** Sign-up must not block the first action ([decision 0003](../decisions/0003-contact-before-signup.md)). *Built.*
4. **Qualifying questionnaire and FAQ on breeder profiles.** Directly targets Ewa's repeated questions and random inquiries. *Built.*
5. **Alerts matched to criteria.** None of the six competitors we compared offers proactive matching across adoption and purchase (desk research of public websites and pricing, 2026-09-19: OLX pets category, Wamiz, Petadopcje, Hodowca.pl, Petopo, PetNest). *Built, under-used in marketing.*
6. **"Still available" freshness signal.** Targets Marta's pain and the main reason people stop trusting the category. *Data exists, no UI yet: the cheapest missing MVP piece.*
7. **Business panel with stats for breeders.** Without it Ewa can't tell whether a higher plan is worth paying for. *Built, three plan tiers.*

Deliberately out of MVP scope ([decision 0004](../decisions/0004-mvp-scope-cuts.md)): cost-of-ownership calculator, mascot, full health profile, services marketplace.

## 5. Success metrics: first 90 days

1. **Active breeders with a complete profile:** 0 → 10+ (leading indicator of supply).
2. **Qualified user-to-partner inquiries:** baseline set after the first pilot, then a weekly target.
3. **Android app live and stable:** internal testing only → production release within 60 days.
4. **End-to-end payment proven:** not confirmed → confirmed within 30 days. Blocker for any MRR conversation.
5. **Active alerts per account:** raw count today → baseline after the Android launch.

## 6. Riskiest assumptions, cheap to test

1. **Breeders will pay for saved time, not just visibility.** Test: 5–8 structured interviews about price and willingness to pay. Cost ≈ 0, 1–2 weeks.
2. **One pilot (a partner breeder plus a pet event) will produce measurable, good-quality contacts at an acceptable cost.** Test: a QR/UTM funnel measuring scans → sign-ups → inquiries. Materials under 500 PLN, results in 2–3 weeks.
3. **Adoption listings next to breeder listings don't make Petsify less attractive to breeders.** Open since 2026-08-12. Test: ask directly in the same interviews. No extra cost.

## 7. Go-to-market: first channels

1. **Industry events with a dedicated QR/UTM.** The cheapest way to reach a concentrated group of high-intent breeders.
2. **Breed groups and breeder-to-breeder referrals.** Our persona notes list referrals and breed groups as the way breeders discover new tools; this still needs confirming in conversations.
3. **SEO on breed pages.** A cheap, long-term channel for the demand side that supports supply through traffic and domain trust.

**CAC.** For breeders (the only segment we plan to charge) cash CAC is close to zero today, but time CAC is high: acquisition happens through direct conversations by me and my GTM partner, not paid ads ("paid performance only after the first data"). An honest PLN figure isn't possible yet.

**Growth idea specific to this product.** Breeders already meet in person at shows and club events. A QR code that leads straight to a ready breeder profile (not a landing page) turns one event into a measurable sign-up → inquiry funnel with no media budget. Repeat it at further events once the pilot proves it works.
