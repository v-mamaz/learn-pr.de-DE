### <a name="exercise-4-create-a-nothotdog-app"></a>Übung 4: Erstellen einer NotHotDog-App

In dieser Übung verwenden Sie [Visual Studio Code](https://code.visualstudio.com/), Microsofts kostenlosen, plattformübergreifenden Quellcode-Editor, der in der Data Science Virtual Machine vorinstalliert ist, um eine NotHotDog-App in Python zu schreiben. Die App verwendet [Tkinter](https://wiki.python.org/moin/TkInter), ein beliebtes GUI-Framework für Python, um die Benutzeroberfläche zu implementieren, und lässt Sie Bilder aus Ihrem lokalen Dateisystem auswählen. Dann übergibt sie diese Bilder dem Modell, das Sie in der vorherigen Übung trainiert haben, und teilt Ihnen mit, ob sie einen Hotdog enthalten.

1. Klicken Sie in der oberen linken Ecke des Desktops auf **Anwendungen**, und wählen Sie **Zubehör > Visual Studio Code** aus, um Visual Studio Code zu starten. Öffnen Sie mit dem Visual Studio Code-Befehl **Datei > Ordner öffnen...** den Ordner „notebooks/tensorflow-for-Poets-2/Tf_files“ mit der Datei **retrained_graph_hotdog.pb**, die Sie beim Trainieren des Modells erstellt haben.

1. Erstellen Sie eine neue Datei namens **classify.py** im aktuellen Ordner. Wenn Visual Studio Code anbietet, die Python-Erweiterung zu installieren, klicken Sie auf **Installieren**. Kopieren Sie den folgenden Code in die Zwischenablage, und fügen Sie ihn mit **UMSCHALT + EINFG** in **classify.py** ein. Speichern Sie dann die Datei:

    ```python
    import tkinter as tk
    from tkinter import messagebox, filedialog, font
    from PIL import ImageTk, Image
    import subprocess

    def select_image_click(img_label):
        try:
            file = filedialog.askopenfilename()

            img = Image.open(file)
            img = img.resize((300, 300))
            selected_img = ImageTk.PhotoImage(img)

            img_label.configure(image=selected_img, width=240)

            output = subprocess.check_output(["python",
                "../scripts/label_image.py",
                "--graph=retrained_graph_hotdog.pb",
                "--image={0}".format(file),
                "--labels=retrained_labels_hotdog.txt"])

            highest = str(output).split("\\n")[3].split(" ")

            if len(highest) == 3:
                score = float(highest[2])
                is_hotdog = True
            else:
                score = float(highest[3])
                is_hotdog = False

            if score > 0.95:
                if is_hotdog:
                    messagebox.showinfo("Result", "That's a hot dog!")
                else:
                    messagebox.showinfo("Result", "That's not a hot dog.")
            else:
                messagebox.showinfo("Result", "Can't tell.")

        except FileNotFoundError as e:
            messagebox.showerror("File not found", "File {0} was not found.".format(e.filename))

    def run():
        window = tk.Tk()

        window.title("Hotdog or Not Hotdog")
        window.geometry('400x600')

        text_font = font.Font(size=18, family="Helvetica Neue")
        welcome_text = tk.Label(window, text="Hot Dog or Not Hot Dog", font=text_font)
        welcome_text.pack()

        instructions_text = tk.Label(window, text="\n\nUse a neural network built with Tensorflow\n"
            "to identify photos containing hot dogs")
        instructions_text.pack(fill=tk.X)

        select_btn = tk.Button(window, text="Select", bg="#0063B1", fg="white", width=5, height=1)
        select_btn.pack(pady=30)

        image_label = tk.Label(window)
        image_label.pack()

        select_btn.configure(command=lambda: select_image_click(image_label))
        window.mainloop()

    if __name__ == "__main__":
        run()
    ```

    Der Schlüsselcode ist hier der Aufruf von ```subprocess.check_output```, wodurch das trainierte Modell durch Ausführung eines Python-Skripts mit dem Namen **label_image.py** aus dem Ordner „scripts“ mit Übergabe des vom Benutzer ausgewählten Bilds aufgerufen wird. Dieses Skript stammt aus dem Repository, das Sie in der vorherigen Übung geklont haben.

1. Suchen Sie mit Ihrer bevorzugten Suchmaschine einige Lebensmittelbilder – einige mit Hotdogs, andere ohne. Laden Sie diese Bilder herunter, und speichern Sie sie im Dateisystem des virtuellen Computers am Speicherort Ihrer Wahl.

1. Öffnen Sie mit dem Visual Studio Code-Befehl **Ansicht > Integriertes Terminal** ein integriertes Terminal. Führen Sie dann den folgenden Befehl in dem integrierten Terminal aus, um die App auszuführen:

     ```bash
     python classify.py
     ```

1. Klicken Sie auf die **Auswählen**-Schaltfläche der App, und wählen Sie eines der Hotdogbilder aus, die Sie in Schritt 3 heruntergeladen haben. Warten Sie, bis ein Meldungsfeld angezeigt wird, das angibt, ob das Bild einen Hotdog enthält. Hat das Modell funktioniert?

    > Fehlermeldungen bezüglich eines fehlenden Kerneltreibers, die im Terminalfenster angezeigt werden, wenn Sie ein Bild verarbeiten, können Sie getrost ignorieren. Sie ergeben sich aus der Tatsache, dass die Data Science Virtual Machine keine virtuelle GPU enthält.

    ![Auswahl eines Bildes](../images/select-image.png)

    _Auswahl eines Bildes_

1. Wiederholen Sie den vorherigen Schritt, mit einem Bild, das keinen Hotdog zeigt. Hat das Modell diesmal funktioniert?

Speisen Sie weiterhin Lebensmittelbilder in die App ein, bis Sie damit zufrieden sind, dass sie Bilder identifizieren kann, die Hotdogs zeigen. Erwarten Sie keine Erfolgsquote von 100%, aber erwarten Sie, dass es *meistens* funktioniert.