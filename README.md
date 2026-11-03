# Wa-sms 3.0 (Rust) — developed by Rocklin K S

Excel (branches + Reviews) + contacts.json / contacts.txt  ->  WhatsApp and/or SMS (phone gateway on the LAN, no login).

## What changed from the Go version
1. No send history. `state.json` is gone, so the "same message already exists" prompt can never appear: any message can be sent again to the same person.
2. WhatsApp links as Google Chrome (Linux) and asks for no chat history (history sync skipped, nothing stored).
3. Whole program rewritten in Rust (one small binary, about 10 MB).

## Screen (five steps, top to bottom; everything is clickable, every button also shows its key)
1. FILES: Browse the Excel file and the contacts file.
2. MESSAGE: Template | Custom. "Edit text" writes the message. With Custom you can also "Choose file" (optional attachment):
   the type is detected from the file content (video -> video, audio -> audio, picture -> image, everything else -> document).
   The custom message is never saved to disk (it lives in memory for this run only).
   Text is the caption (audio: text follows as its own message). SMS carries the text only.
3. SEND VIA: tick WhatsApp, SMS, or both. "Test SMS gateway" checks the phone app (sends no SMS). "Link WhatsApp" shows the QR / pairing code.
4. SEND TO: one tick per role (BM, ASM, CRM, AGM ...). Only ticked roles get the message. If AGM is not ticked but looks after the ticked branches you are asked once: "Also send to AGM?" Nothing else is offered.
5. BRANCHES: the branches with 0 reviews are listed in the box on the right (click it to copy/save the list). Click rows to tick them, or Select all / Unselect all.
Then click the big green SEND button (it says what is still missing until you are ready; it becomes a red STOP button while sending).
Bottom bar: Theme (pick a colour theme, default Catppuccin Mocha blue), Settings, Contacts, 0 Reviews, Reload, Help, Quit.
Keys: W S M E F B K A N G 1-9 T O C Z R L H, Space tick row, Ctrl+S / F5 send, Esc stop, Ctrl+Q quit.

## Run
    chmod +x wa-sms
    ./wa-sms              # ./wa-sms install  adds an applications-menu entry, ./wa-sms uninstall removes it

Needs 64-bit Linux with glibc 2.39 or newer. Data folder: `WA_SMS_DATA`, else `data` next to the program, else `~/.local/share/wa-sms`.
`config.json` and the contacts files are compatible with the Go version. Link WhatsApp once again (F9): the old Go session is not compatible.
Keep `whatsapp-session.db` private like a password and never publish your contacts.

## Build from source
    tar xzf wa-sms-src.tar.gz && cd wa-sms && cargo build --release     # stable Rust; result: target/release/wa-sms
