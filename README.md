productes = []

    while True:
        print("--- SUPERMERCAT PEDROSA ---")
        print("1. Afegir un producte")
        print("2. Eliminar un producte")
        print("3. Modificar un producte (Nom, Preu o Quantitat)")
        print("4. Llistar els productes")
        print("5. Mostrar estadístiques (Total productes i Valor estoc)")
        print("6. Sortir")

    opcio = input("Tria una opció: ")

    # 1. AFEGIR PRODUCTE (Amb control de duplicats)
    if opcio == "1":
        nom = input("Nom del producte: ").capitalize()  # Capitalize para que 'Poma' y 'poma' sean lo mismo

        # Comprovem si ja existeix
        existeix = False
        for p in productes:
            if p[0] == nom:
                existeix = True
                break

        if existeix:
            print(f"ERROR: El producte '{nom}' ja existeix!")
        else:
            preu = float(input("Preu: "))
            quantitat = int(input("Quantitat: "))
            # Guardem com a llista [nom, preu, quantitat]
            productes.append([nom, preu, quantitat])
            print("Producte afegit correctament!")

    # 2. ELIMINAR PRODUCTE
    elif opcio == "2":
        nom_buscar = input("Nom del producte a eliminar: ").capitalize()
        encontrado = False
        for p in productes:
            if p[0] == nom_buscar:
                productes.remove(p)
                print("Eliminat correctament.")
                encontrado = True
                break
        if not encontrado:
            print("No s'ha trobat el producte.")

    # 3. MODIFICAR (Nom, Preu o Quantitat - Extra 1 i 2)
    elif opcio == "3":
        nom_buscar = input("Nom del producte a modificar: ").capitalize()
        encontrado = False
        for p in productes:
            if p[0] == nom_buscar:
                print(f"Trobat: {p[0]} | Preu: {p[1]}€ | Qty: {p[2]}")
                canvi = input("Què vols canviar? (nom/preu/quantitat): ").lower()

                if canvi == "nom":
                    nou_nom = input("Nou nom: ").capitalize()
                    # Aquí podries afegir una comprovació extra de duplicats si vols ser molt estricte
                    p[0] = nou_nom
                elif canvi == "preu":
                    p[1] = float(input("Nou preu: "))
                elif canvi == "quantitat":
                    p[2] = int(input("Nova quantitat: "))
                else:
                    print("Opció no vàlida.")

                print("Modificat correctament!")
                encontrado = True
                break
        if not encontrado:
            print("No s'ha trobat el producte.")

    # 4. LLISTAR PRODUCTES
    elif opcio == "4":
        print("\n--- LLISTA DE PRODUCTES ---")
        if len(productes) == 0:
            print("La llista està buida.")
        else:
            for p in productes:
                valor_producte = p[1] * p[2]
                print(f"Producte: {p[0]} | Preu: {p[1]}€ | Quantitat: {p[2]} | Valor Total: {valor_producte:.2f}€")

    # 5. ESTADÍSTIQUES (Requeriment base + Extra 2 Valor Total)
    elif opcio == "5":
        total_referencies = len(productes)
        valor_total_estoc = 0

        for p in productes:
            # Sumem (Preu * Quantitat) de cada producte
            valor_total_estoc += (p[1] * p[2])

        print(f"\nProductes diferents: {total_referencies}")
        print(f"Valor total de l'estocatge: {valor_total_estoc:.2f}€")

    # 6. SORTIR
    elif opcio == "6":
        print("Adéu!")
        break

    else:
        print("Opció no vàlida, torna-ho a provar.")
