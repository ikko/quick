# **Nano Editor Keyboard Shortcuts Handbook**  
Nano is a simple, easy-to-use terminal-based text editor for Linux. Below is a **comprehensive handbook** of its keyboard shortcuts, grouped by functionality.  

---

## **1. Basics**  

| **Shortcut** | **Action**                      |
|--------------|---------------------------------|
| `nano <file>`| Open a file in Nano             |
| `Ctrl + X`   | Exit Nano                       |
| `Ctrl + O`   | Write (save) changes to a file  |
| `Ctrl + G`   | Show help screen                |
| `Ctrl + T`   | Open spell checker              |
| `Ctrl + R`   | Insert another file into the current file |
| `Ctrl + W`   | Search for text                 |
| `Ctrl + \`   | Replace text                    |

---

## **2. Navigation**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + A`         | Move to the beginning of the line       |
| `Ctrl + E`         | Move to the end of the line             |
| `Ctrl + Y`         | Move up a screen (page up)              |
| `Ctrl + V`         | Move down a screen (page down)          |
| `Ctrl + _`         | Move to a specific line and column      |
| `Ctrl + Space`     | Move forward one word                   |
| `Alt + Space`      | Move backward one word                  |
| `Ctrl + P`         | Move to the previous line               |
| `Ctrl + N`         | Move to the next line                   |

---

## **3. Editing Text**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + K`         | Cut (delete) the current line           |
| `Ctrl + U`         | Paste (uncut) text                     |
| `Ctrl + J`         | Justify the current paragraph           |
| `Ctrl + T`         | Invoke spell checker                    |
| `Alt + U`          | Undo last action                       |
| `Alt + E`          | Redo undone action                     |
| `Ctrl + D`         | Delete character under the cursor       |
| `Ctrl + H`         | Delete character to the left of cursor  |
| `Alt + T`          | Cut from cursor to end of paragraph     |
| `Ctrl + I`         | Insert a tab at the cursor position     |

---

## **4. Search and Replace**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + W`         | Search for text                         |
| `Ctrl + W` → `Ctrl + R` | Repeat last search                 |
| `Alt + W`          | Search backwards                       |
| `Ctrl + \`         | Replace text                           |
| `Alt + R`          | Start the replacement (after prompt)    |

---

## **5. Marking and Cutting Text**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + ^`         | Mark text at the current cursor position|
| `Ctrl + K`         | Cut marked text                        |
| `Ctrl + U`         | Paste (uncut) text                     |

**Tip**: Use `Ctrl + ^` to start marking and then navigate with movement shortcuts.

---

## **6. Managing Files**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + O`         | Save the file                          |
| `Ctrl + X`         | Exit Nano                              |
| `Ctrl + R`         | Read a file into the current file      |
| `Alt + F`          | Open a file browser                    |

---

## **7. Scrolling and Navigation within File**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + V`         | Scroll down one page                   |
| `Ctrl + Y`         | Scroll up one page                     |
| `Ctrl + C`         | Show current cursor position           |
| `Ctrl + _`         | Jump to a specific line and column     |

---

## **8. Indentation and Formatting**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + I`         | Insert a tab                           |
| `Alt + }`          | Indent marked lines                    |
| `Alt + {`          | Unindent marked lines                  |
| `Ctrl + J`         | Justify the current paragraph          |

---

## **9. Nano Settings and Configuration**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Alt + X`          | Toggle soft line wrapping              |
| `Alt + L`          | Toggle line numbers                    |
| `Alt + M`          | Toggle mouse support                   |
| `Alt + N`          | Toggle line numbering                  |
| `Alt + P`          | Toggle whitespace display              |

---

## **10. Miscellaneous Shortcuts**  

| **Shortcut**      | **Action**                              |
|--------------------|-----------------------------------------|
| `Ctrl + L`         | Refresh the screen                     |
| `Ctrl + C`         | Display cursor position                |
| `Ctrl + Z`         | Suspend Nano (returns to terminal)     |
| `Ctrl + X`         | Close Nano                             |
| `Ctrl + G`         | Show the help menu                     |

---

## **11. Nano Configuration File**

You can customize Nano settings by editing its configuration file:  
- System-wide: `/etc/nanorc`  
- User-specific: `~/.nanorc`

### Example `.nanorc` Configuration
```bash
set linenumbers       # Show line numbers  
set mouse             # Enable mouse support  
set softwrap          # Wrap long lines  
set tabsize 4         # Set tab size to 4 spaces  
set nowrap            # Disable text wrapping  
```

To reload the configuration, restart Nano.

---

## **12. Example Workflow**

Here’s a step-by-step Nano workflow:  

1. **Open a File**  
   ```bash
   nano myfile.txt
   ```  

2. **Edit the File**  
   - Navigate: `Ctrl + N` / `Ctrl + P`  
   - Delete: `Ctrl + K`  
   - Paste: `Ctrl + U`  
   - Search: `Ctrl + W`  
   - Replace: `Ctrl + \`  

3. **Save Changes**  
   - Press `Ctrl + O`, then `Enter` to confirm.  

4. **Exit**  
   - Use `Ctrl + X` to exit. If changes are unsaved, Nano will prompt you to save.

---

## **13. Tips for Efficient Usage**  

1. **Mark and Cut**: Use `Ctrl + ^` to start marking and `Ctrl + K` to cut.  
2. **Mouse Support**: Enable it with `Alt + M` or in `.nanorc`.  
3. **Jump to Line**: Use `Ctrl + _` for direct navigation.  
4. **Configuration**: Customize Nano behavior in `~/.nanorc` for frequent settings.  
5. **Justify Text**: Automatically format paragraphs with `Ctrl + J`.

---

## **14. Nano vs Other Editors**  

| **Feature**         | **Nano**              | **Vim**          | **Emacs**        |
|----------------------|-----------------------|------------------|------------------|
| Ease of Use          | Very easy             | Steep learning   | Moderate learning|
| Default Availability | Always preinstalled   | Often available  | Usually requires |
| GUI Support          | No                    | Limited          | Yes              |
| Complexity           | Simple                | Advanced         | Highly advanced  |

---

## **15. Resources**  

- **Official Nano Documentation**: [https://www.nano-editor.org/](https://www.nano-editor.org/)  
- **Man Page**: Access via terminal with:  
  ```bash
  man nano
  ```  

---

With this cheatsheet, you can efficiently use **Nano** for quick and lightweight text editing in Linux!
