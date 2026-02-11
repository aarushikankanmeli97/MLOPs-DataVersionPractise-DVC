---

# 📦 DVC Practice Project

This project demonstrates a hands-on workflow to understand how **DVC (Data Version Control)** works alongside **Git** for versioning data.

⚠️ **Note:** In this project, `S3` is **not an actual AWS S3 bucket**.
It is simply a **local folder named `S3`** created to act as a remote storage location for DVC.

---

## 🎯 Objective

* Track data using DVC instead of Git
* Configure a DVC remote (local folder named `S3`)
* Maintain multiple versions of data
* Understand how Git and DVC work together

---

## 🛠️ Project Workflow

Below are the exact steps followed in this practice project.

---

## 1️⃣ Initialise Git Repository

1. Create a new Git repository.
2. Clone it locally.

```bash
git clone <repo-url>
cd <repo-name>
```

---

## 2️⃣ Create `main.py`

* Create a file named `main.py`.
* Add code to it.
* The script saves a CSV file into a folder named:

```
data/
```

---

## 3️⃣ Commit Before Initialising DVC

Before introducing DVC, commit the project using Git:

```bash
git add .
git commit -m "Initial commit before DVC"
git push
```

Then install DVC:

```bash
pip install dvc
```

---

## 4️⃣ Initialise DVC

Initialise DVC in the repository:

```bash
dvc init
```

This creates:

* `.dvc/` directory
* `.dvcignore` file

---

## 5️⃣ Create Dummy `S3` Folder

Create a folder named:

```
S3/
```

This folder will act as the DVC remote storage location.
It is **not an AWS S3 bucket**, just a local directory.

---

## 6️⃣ Configure DVC Remote

Direct DVC to use the local `S3` folder as remote storage:

```bash
dvc remote add -d myremote S3
```

This sets `myremote` as the default remote.

---

## 7️⃣ Add Data Folder to DVC

Run:

```bash
dvc add data/
```

An error appears asking to execute:

```bash
git rm -r --cached 'data'
git commit -m "stop tracking data"
```

### Why?

Initially, the `data/` folder was tracked by Git.
Since DVC will now manage this folder, Git must stop tracking it.

---

## 8️⃣ Re-Add Data to DVC

After removing Git tracking, run:

```bash
dvc add data/
```

This creates:

```
data.dvc
```

Then stage the necessary files:

```bash
git add .gitignore data.dvc
```

---

## 9️⃣ Commit Data to DVC Remote

```bash
dvc commit
dvc push
```

This pushes the tracked data to the local `S3/` folder configured as the remote.

---

## 🔟 Save First Version (V1)

Commit everything in Git to mark this as **Version 1 of data**:

```bash
git add .
git commit -m "Data Version 1"
git push
```

---

## 1️⃣1️⃣ Modify Data (V2)

* Modify `main.py` to append a new row to the CSV file.
* Run the script to update the data.

Check changes:

```bash
dvc status
```

---

## 1️⃣2️⃣ Commit & Push Updated Data

```bash
dvc commit
dvc push
```

---

## 1️⃣3️⃣ Save Second Version (V2)

```bash
git add .
git commit -m "Data Version 2"
git push
```

At this stage, **Version 2** of the data is saved.

---

## 1️⃣4️⃣ Verify Status

Check Git and DVC status:

```bash
git status
dvc status
```

Everything should be up to date.

---

## 1️⃣5️⃣ Repeat for Version 3 (V3)

Repeat steps 10–12:

* Modify data
* `dvc status`
* `dvc commit`
* `dvc push`
* `git add-commit-push`

This saves **Version 3 of the data**.

---

# 🔄 Versioning Summary

| Version | Action Taken             |
| ------- | ------------------------ |
| V1      | Initial DVC tracked data |
| V2      | Appended new row to CSV  |
| V3      | Further data update      |

Each version:

* Is tracked by **DVC**
* Stored in the local `S3/` folder
* Version-controlled via **Git commits**

---

# 📚 Key Learnings

* Git should not track data once DVC manages it.
* DVC tracks data files while Git tracks `.dvc` metadata files.
* `dvc add` creates a `.dvc` file that Git tracks.
* `dvc commit` updates DVC cache.
* `dvc push` transfers data to the configured remote.
* Git commits represent different stages of data versions.

---

# ✅ Final State

* Git tracks:

  * `main.py`
  * `data.dvc`
  * `.dvc` configuration files

* DVC tracks:

  * `data/` folder

* Local `S3/` folder stores:

  * All versions of the dataset

---

This project demonstrates a complete workflow of integrating **Git + DVC** with a locally configured remote folder (`S3/`) for structured data versioning.

