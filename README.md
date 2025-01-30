

## Umbrel Community App Store Template

To repozytorium jest szablonem do tworzenia społecznościowego sklepu z aplikacjami dla Umbrel. Dzięki tym dodatkowym sklepom deweloperzy mogą dystrybuować aplikacje bez konieczności przesyłania ich do oficjalnego sklepu Umbrel App Store.

Wystarczy kliknąć przycisk „Use this template” (Użyj tego szablonu) powyżej i rozpocząć dodawanie własnych aplikacji!

### Technical Details

Plik `umbrel-app-store.yml` definiuje dwie ważne właściwości:
- `id` - Jest używane jako prefiks dla wszystkich aplikacji w społecznościowym sklepie z aplikacjami. MUSISZ dodać identyfikator swojego sklepu jako prefiks do identyfikatora aplikacji. Na przykład, jeśli ten szablon definiuje `sparkles` jako identyfikator sklepu, a aplikacja nazywa się `hello world`, to jej identyfikator powinien wyglądać tak: `sparkles-hello-world`
- `name` - Ta nazwa będzie wyświetlana w interfejsie użytkownika Umbrel, gdy użytkownicy przeglądają aplikacje w społecznościowych sklepach z aplikacjami.


### Testing

Aby przetestować swój społecznościowy sklep z aplikacjami, możesz dodać to repozytorium poprzez interfejs użytkownika Umbrel, zgodnie z poniższym pokazem demonstracyjnym:


https://user-images.githubusercontent.com/10330103/197889452-e5cd7e96-3233-4a09-b475-94b754adc7a3.mp4


Alternatywnie możesz użyć Umbrel CLI, jak opisano poniżej.

Aby dodać sklep z aplikacjami:
```
sudo ~/umbrel/scripts/repo add https://github.com/getumbrel/umbrel-community-app-store.git
sudo ~/umbrel/scripts/repo update
```

Aby zainstalować aplikację ze sklepu z aplikacjami:
```
sudo ~/umbrel/scripts/app install sparkles-hello-world
```

Aby usunąć sklep z aplikacjami:
```
sudo ~/umbrel/scripts/repo remove https://github.com/getumbrel/umbrel-community-app-store.git
```
2 changes: 2 additions & 0 deletions 2
umbrel-app-store.yml
@@ -0,0 +1,2 @@
id: "sparkles" # Choose the ID for your app store. This should contain only alphabets ("a to z") and dashes ("-").
name: "Sparkles" # Choose the name of your app store. It will show up in the UI as "<name> App Store".
0 comments on commit d074338
@marciasmedia
Comment

Leave a comment
Footer
© 2024 GitHub, Inc.
Footer navigation

    Terms
    Privacy
    Security
    Status
    Docs
    Contact

Add files via upload · marciasmedia/umbrell-app@d074338
