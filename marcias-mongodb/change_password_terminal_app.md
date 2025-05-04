1. **Zmiana bazy danych na admin**:  
Aby upewnić się, że masz dostęp do bazy admin (gdzie są przechowywani użytkownicy i hasła), wpisz:

    ```bash
    use admin
    ```

2. **Zmiana hasła użytkownika root**:  
Teraz, jeśli chcesz zmienić hasło użytkownika root, możesz to zrobić za pomocą poniższej komendy:

    ```bash
    db.changeUserPassword("root", "nowe_hasło")
    ```