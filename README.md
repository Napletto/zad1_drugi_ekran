<img width="605" height="1264" alt="image" src="https://github.com/user-attachments/assets/0f443ece-1bea-4bde-9aff-524f9e95cf91" />
<img width="601" height="1279" alt="image" src="https://github.com/user-attachments/assets/4486a7ea-6ec0-4519-b12d-6d4b9ccc373b" />

**Dlaczego rejestracja wyniku jest polem klasy, a nie znajduje się w obsłudze kliknięcia przycisku?**

`registerForActivityResult` musi zostać wywołane, zanim ekran przejdzie w stan STARTED.
Wywołane w obsłudze kliknięcia kończy się wyjątkiem „LifecycleOwners must call register
before they are STARTED". Jest też powód praktyczny: gdy system zniszczy i odtworzy ekran,
rejestracja musi już istnieć, zanim wróci wynik z otwartego wcześniej ekranu. Rejestracja
w polu klasy spełnia ten warunek zawsze.

**Co zobaczy ekran wywołujący, gdy użytkownik naciśnie na drugim ekranie przycisk Wstecz?**

Sprawdzone na emulatorze: nic się nie dzieje, formularz zostaje wypełniony, a Snackbar
nie pojawia się. Ekran wywołujący dostaje `RESULT_CANCELED` (ustawiane automatycznie,
gdy nie wywołano `setResult`), a `result.getData()` jest `null`. Warunek w callbacku
sprawdza `RESULT_OK`, więc kod w środku się nie wykonuje.
