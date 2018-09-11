### <a name="exercise-4-create-a-nothotdog-app"></a><span data-ttu-id="53e1c-101">Übung 4: Erstellen einer NotHotDog-App</span><span class="sxs-lookup"><span data-stu-id="53e1c-101">Exercise 4: Create a NotHotDog app</span></span>

<span data-ttu-id="53e1c-102">In dieser Übung verwenden Sie [Visual Studio Code](https://code.visualstudio.com/), Microsofts kostenlosen, plattformübergreifenden Quellcode-Editor, der in der Data Science Virtual Machine vorinstalliert ist, um eine NotHotDog-App in Python zu schreiben.</span><span class="sxs-lookup"><span data-stu-id="53e1c-102">In this exercise, you will use [Visual Studio Code](https://code.visualstudio.com/), Microsoft's free, cross-platform source-code editor which is preinstalled in the Data Science VM, to write a NotHotDog app in Python.</span></span> <span data-ttu-id="53e1c-103">Die App verwendet [Tkinter](https://wiki.python.org/moin/TkInter), ein beliebtes GUI-Framework für Python, um die Benutzeroberfläche zu implementieren, und lässt Sie Bilder aus Ihrem lokalen Dateisystem auswählen.</span><span class="sxs-lookup"><span data-stu-id="53e1c-103">The app will use [Tkinter](https://wiki.python.org/moin/TkInter), which is a popular GUI framework for Python, to implement its user interface, and it will allow you to select images from your local file system.</span></span> <span data-ttu-id="53e1c-104">Dann übergibt sie diese Bilder dem Modell, das Sie in der vorherigen Übung trainiert haben, und teilt Ihnen mit, ob sie einen Hotdog enthalten.</span><span class="sxs-lookup"><span data-stu-id="53e1c-104">Then it will pass those images to the model you trained in the previous exercise and tell you whether they contain a hot dog.</span></span>

1. <span data-ttu-id="53e1c-105">Klicken Sie in der oberen linken Ecke des Desktops auf **Anwendungen**, und wählen Sie **Zubehör > Visual Studio Code** aus, um Visual Studio Code zu starten.</span><span class="sxs-lookup"><span data-stu-id="53e1c-105">Click **Applications** in the upper-left corner of the desktop and select **Accessories > Visual Studio Code** to start Visual Studio Code.</span></span> <span data-ttu-id="53e1c-106">Öffnen Sie mit dem Visual Studio Code-Befehl **Datei > Ordner öffnen...** den Ordner „notebooks/tensorflow-for-Poets-2/Tf_files“ mit der Datei **retrained_graph_hotdog.pb**, die Sie beim Trainieren des Modells erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="53e1c-106">Use Visual Studio Code's **File > Open Folder...** command to open the "notebooks/tensorflow-for-poets-2/tf_files" folder containing the **retrained_graph_hotdog.pb** file created when you trained the model.</span></span>

1. <span data-ttu-id="53e1c-107">Erstellen Sie eine neue Datei namens **classify.py** im aktuellen Ordner.</span><span class="sxs-lookup"><span data-stu-id="53e1c-107">Create a new file named **classify.py** in the current folder.</span></span> <span data-ttu-id="53e1c-108">Wenn Visual Studio Code anbietet, die Python-Erweiterung zu installieren, klicken Sie auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="53e1c-108">If Visual Studio Code offers to install the Python extension, click **Install** to install it.</span></span> <span data-ttu-id="53e1c-109">Kopieren Sie den folgenden Code in die Zwischenablage, und fügen Sie ihn mit **UMSCHALT + EINFG** in **classify.py** ein.</span><span class="sxs-lookup"><span data-stu-id="53e1c-109">Copy the code below to the clipboard and use **Shift+Ins** to paste it into **classify.py**.</span></span> <span data-ttu-id="53e1c-110">Speichern Sie dann die Datei:</span><span class="sxs-lookup"><span data-stu-id="53e1c-110">Then save the file:</span></span>

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

    <span data-ttu-id="53e1c-111">Der Schlüsselcode ist hier der Aufruf von ```subprocess.check_output```, wodurch das trainierte Modell durch Ausführung eines Python-Skripts mit dem Namen **label_image.py** aus dem Ordner „scripts“ mit Übergabe des vom Benutzer ausgewählten Bilds aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="53e1c-111">They key code here is the call to ```subprocess.check_output```, which invokes the trained model by executing a Python script named **label_image.py** found in the "scripts" folder, passing in the image that the user selected.</span></span> <span data-ttu-id="53e1c-112">Dieses Skript stammt aus dem Repository, das Sie in der vorherigen Übung geklont haben.</span><span class="sxs-lookup"><span data-stu-id="53e1c-112">This script came from the repo that you cloned in the previous exercise.</span></span>

1. <span data-ttu-id="53e1c-113">Suchen Sie mit Ihrer bevorzugten Suchmaschine einige Lebensmittelbilder – einige mit Hotdogs, andere ohne.</span><span class="sxs-lookup"><span data-stu-id="53e1c-113">Use your favorite search engine to find a few food images — some containing hot dogs, and some not.</span></span> <span data-ttu-id="53e1c-114">Laden Sie diese Bilder herunter, und speichern Sie sie im Dateisystem des virtuellen Computers am Speicherort Ihrer Wahl.</span><span class="sxs-lookup"><span data-stu-id="53e1c-114">Download these images and store them in the location of your choice in the VM's file system.</span></span>

1. <span data-ttu-id="53e1c-115">Öffnen Sie mit dem Visual Studio Code-Befehl **Ansicht > Integriertes Terminal** ein integriertes Terminal.</span><span class="sxs-lookup"><span data-stu-id="53e1c-115">Use Visual Studio Code's **View > Integrated Terminal** command to open an integrated terminal.</span></span> <span data-ttu-id="53e1c-116">Führen Sie dann den folgenden Befehl in dem integrierten Terminal aus, um die App auszuführen:</span><span class="sxs-lookup"><span data-stu-id="53e1c-116">Then execute the following command in the integrated terminal to run the app:</span></span>

     ```bash
     python classify.py
     ```

1. <span data-ttu-id="53e1c-117">Klicken Sie auf die **Auswählen**-Schaltfläche der App, und wählen Sie eines der Hotdogbilder aus, die Sie in Schritt 3 heruntergeladen haben.</span><span class="sxs-lookup"><span data-stu-id="53e1c-117">Click the app's **Select** button and pick one of the hot-dog images you downloaded in Step 3.</span></span> <span data-ttu-id="53e1c-118">Warten Sie, bis ein Meldungsfeld angezeigt wird, das angibt, ob das Bild einen Hotdog enthält.</span><span class="sxs-lookup"><span data-stu-id="53e1c-118">Wait for a message box to appear, indicating whether the image contains a hot dog.</span></span> <span data-ttu-id="53e1c-119">Hat das Modell funktioniert?</span><span class="sxs-lookup"><span data-stu-id="53e1c-119">Did the model get it correct?</span></span>

    > <span data-ttu-id="53e1c-120">Fehlermeldungen bezüglich eines fehlenden Kerneltreibers, die im Terminalfenster angezeigt werden, wenn Sie ein Bild verarbeiten, können Sie getrost ignorieren.</span><span class="sxs-lookup"><span data-stu-id="53e1c-120">If you see error messages regarding a missing kernel driver in the terminal window when you process an image, you can safely ignore them.</span></span> <span data-ttu-id="53e1c-121">Sie ergeben sich aus der Tatsache, dass die Data Science Virtual Machine keine virtuelle GPU enthält.</span><span class="sxs-lookup"><span data-stu-id="53e1c-121">They result from the fact that the Data Science VM does not contain a virtual GPU.</span></span>

    ![Auswahl eines Bildes](../images/select-image.png)

    <span data-ttu-id="53e1c-123">_Auswahl eines Bildes_</span><span class="sxs-lookup"><span data-stu-id="53e1c-123">_Selecting an image_</span></span>

1. <span data-ttu-id="53e1c-124">Wiederholen Sie den vorherigen Schritt, mit einem Bild, das keinen Hotdog zeigt.</span><span class="sxs-lookup"><span data-stu-id="53e1c-124">Repeat the previous step using an image that doesn't contain a hot dog.</span></span> <span data-ttu-id="53e1c-125">Hat das Modell diesmal funktioniert?</span><span class="sxs-lookup"><span data-stu-id="53e1c-125">Was the model right this time?</span></span>

<span data-ttu-id="53e1c-126">Speisen Sie weiterhin Lebensmittelbilder in die App ein, bis Sie damit zufrieden sind, dass sie Bilder identifizieren kann, die Hotdogs zeigen.</span><span class="sxs-lookup"><span data-stu-id="53e1c-126">Continue feeding food images into the app until you're satisfied that it can identify images containing hot dogs.</span></span> <span data-ttu-id="53e1c-127">Erwarten Sie keine Erfolgsquote von 100%, aber erwarten Sie, dass es *meistens* funktioniert.</span><span class="sxs-lookup"><span data-stu-id="53e1c-127">Don't expect it to be right 100% of the time, but do expect it to be right *most* of the time.</span></span>