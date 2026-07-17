# DosDos

A desktop app that generates a formal opening greeting for a thesis defense (sidang skripsi). It randomly picks one lecturer as the examiner (penguji) and looks up a specific lecturer as the supervisor (pembimbing), then displays the full greeting in a resizable dark-themed window.
This project is written in [Lateralus](https://lateralus.dev/) (`.ltl`) and compiled to Python.

## What It Does

1. Loads all lecturer data from dosen.json.
2. Randomly selects one lecturer as the penguji (examiner).
3. Looks up a hardcoded lecturer (externaL_SYSTEM_ID = "D5850") as the pembimbing (supervisor).
4. Builds a formal Indonesian greeting:
   > *"Yang terhormat, Bapak/Ibu [penguji] selaku penguji sidang skripsi hari ini.*  
   > *Yang saya hormati, Bapak/Ibu [pembimbing] selaku Dosen Pembimbing saya, yang telah banyak memberikan bimbingan dan arahan hingga skripsi ini dapat diselesaikan."*
5. Displays the greeting in a 600x400 dark window with center-aligned, auto-wrapping text.

## Requirements

- Python 3.x
- [`customtkinter`](https://github.com/TomSchimansky/CustomTkinter)

```bash
pip install customtkinter
```

## Data Format

```json
[
  {
    "externaL_SYSTEM_ID": "DXXX",
    "n_OFFICIAL_NM": "John Doe, Ph.D.",
    "descr": "XXXX",
    "descR2": "XXXXX",
    "emplid": "BNXXXXX"
  }
]
```

The `externaL_SYSTEM_ID` field is now used to find the supervisor.

## Key Functions

| Function | Purpose |
|---|---|
| `get_pembimbing_name(dosen_list, target_id)` | Searches the list for a lecturer matching the given `externaL_SYSTEM_ID` and returns their `n_OFFICIAL_NM`. Returns `"Nama tidak ditemukan"` if not found. |
| `main()` | Orchestrates the data loading, random selection, greeting construction, and GUI. |

## GUI Behaviour

- **Window size:** 600×400 (minimum 400×300).
- **Text:** Displayed centered in the window, font size 24, with automatic line wrapping that adjusts when the window is resized.
- Close the window to exit — no buttons or timers.

## Customisation

To change the supervisor, edit the ID on this line:

```
let pembimbing = get_pembimbing_name(dosen_data, "D5850")
```

Replace `"D5850"` with the `externaL_SYSTEM_ID` of your actual supervisor.
