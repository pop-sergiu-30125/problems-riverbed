## 1. Bug-urile găsite

Pentru fiecare bug, scrie 2-3 propoziții:

### Bug #1
- **Unde era:** main.py, linia 32
- **Cum l-am găsit:** După ce am rulat pentru prima dată testele, am văzut că testul test_create_event_returns_201, eșua, după care am mers în aplicația de testare să văd ce răspuns primesc (200)
- **Cum l-am fixat:**

### Bug #2
- **Unde era:** storage.py, linia 55
- **Cum l-am găsit:** testul test_list_events_includes_created_items eșua, și am observat că la assertEquals avea ca rezultat 4==5, ceea ce însemna că la capetele listei, un eveniment era ignorat
- **Cum l-am fixat:**

### Bug #3
- **Unde era:** storage.py, linia 51-54
- **Cum l-am găsit:** testul test_list_events_hides_soft_deleted_items eșua, după care am testat endpoint-urile DELETE /events/{event_id} și GET /events, am văzut că evenimentul apare în baza de date, cu data de ștergere
- **Cum l-am fixat:** am adăugat o filtrare, care să meargă prin toată baza de date și să memoreze evenimentele care nu au dată de ștergere

### Bug #4
- **Unde era:** main.py, linia 51-55
- **Cum l-am găsit:** testul legat de schimbarea erorii la a doua ștergere a unui eveniment eșua, după care am testat acel endpoint
- **Cum l-am fixat:** am adăugat o condiție care să verifice dacă un eveniment are deja o dată de ștergere (ceea ce înseamnă că a fost ștearsă cel puțin odată)

---

## 2. Endpoint-ul nou

- **Decizii de design:** (ce-ai considerat? ce ai ales și de ce?)
- **Cazuri edge pe care le-ai acoperit:**
- **Teste adăugate:** primul test verifică dacă filtrarea este executată cum trebuie, iar al doilea test verifică dacă, după filtrare, sunt ignorate și evenimentele care au fost șterse.

---

## 3. Folosirea AI-ului

Fii cinstit. Nu pierzi puncte dacă spui adevărul, dimpotrivă.

- **Ce ai folosit:** Gemini
- **Prompturi reprezentative folosite:** 
1. "can you generate me a test that has two users, and the first one has an older event and a newer event, (an older date like since, so maybe 1/1/2026, like the functions that i've added in main)"
2. "after adding this part if event.deleted_at is not None:
raise HTTPException(status_code=404, detail="Event already deleted") more tests are failing, even the ones i solved

- **Unde te-a ajutat cel mai mult:** La finisarea unor bucăți de cod, la care îi spuneam idea mea de ce aș dori să facă
- **Unde te-a încurcat sau ți-a dat un răspuns greșit:** când am încercat să fac un test pentru filtrarea evenimentelor după dată, nu reușea să găsească o eroare pe care am făcut-o eu (la storage, am scris user.id în loc de user_id), și primeam diferite metode de a repara eroarea, care nu ajutau
- **Cum ai verificat ce-a generat:** prima dată rulând testele, iar dacă rezultatul a fost satisfăcător, am trecut la testările prin endpoint-uri
- **Anexă opțională — export chat:** 

---

## 4. Ce-ai face cu mai mult timp

(Lista scurtă, 3-5 puncte. Arată-ne că ai văzut limitele actuale.)
- o centralizare/automatizare a acelor evenimente ale utilizatorilor, adică acesta să poată prima data executa o operație de login...
- tot aici, partea in care ne conectăm la un cont, și atunci când facem post la un eveniment, să il facem pe contul conectat (la fișiere json nu mai introducem user_id)
- introducere mai multe layere de acces (user, admin)

---

## 5. Întrebări / observații

(Orice nu a fost clar, orice ai vrea să discuți cu noi.)
