---
component: File upload
id-prefix: UPL
status: draft
---

# File upload

## 1. When to use it vs alternatives

- **File upload**: the user provides files from their device.
- **Text input with a link**: a file that already lives online.
- **Image or media picker**: when a gallery of existing assets is chosen from.
- Prefer a native file selection control for the basic case, and add the rest on top of it.

## 2. Anatomy and variants

Parts: label, file selection control, optional drop area, accepted types and size hint, list of files with name, size, status and actions, optional progress, error messages.

Variants that change which capabilities apply:

- Single vs multiple files
- Immediate upload vs upload on form submit
- With vs without drag and drop
- With previews (images)
- New upload only vs showing and replacing files already stored

## 3. States

Empty, files selected, uploading, uploaded, failed, canceled, removed, drag over, disabled, error (rejected file).

## 4. Behavior and keyboard interaction

| Key | Result |
|---|---|
| Tab | Reaches the selection control, then the per-file actions |
| Enter / Space | Opens the file selection |

Everything that can be done by dragging can be done without dragging.

## 5. Component-specific accessibility

- The control has a name, and the accepted types and limits are in text associated with it.
- Status changes (added, uploading, done, failed, removed) are announced.
- Each file action has a name that includes the file name.
- General rules are in the `accessibility` skill.

## 6. Capabilities and edge cases

| ID | Capability | Applies when | Obligation | Owner |
|---|---|---|---|---|
| UPL-01 | Files can be chosen from the device by pointer and keyboard | Always | Required | Usually provided by primitives |
| UPL-02 | A visible drop target with feedback exists, and the same result is reachable without dragging | Drag and drop | If applicable | Application's job |
| UPL-03 | Accepted types and size are stated before selection, enforced on selection, and rejected files get a specific message each | Always | Required | Application's job |
| UPL-04 | A list shows each file with name, size, status and a remove action, and the number of files is limited | Multiple files | If applicable | Application's job |
| UPL-05 | Progress is shown per file and announced | Immediate upload | If applicable | Application's job |
| UPL-06 | An upload in progress can be canceled | Immediate upload | If applicable | Application's job |
| UPL-07 | A failed upload can be retried, and one failure does not lose the others | Multiple files | If applicable | Application's job |
| UPL-08 | Selecting the same file again after removing it works, and duplicates are handled as decided | Always | Required | Application's job |
| UPL-09 | Empty files, very large files, unusual names (unicode, very long, no extension, special characters) and a mismatch between extension and content are handled | Always | Required | Application's job |
| UPL-10 | Image previews are shown and released correctly | Previews | Optional | Application's job |
| UPL-11 | Existing stored files are shown and can be replaced or removed | Editing existing data | If applicable | Application's job |
| UPL-12 | The server validates type, size and content, and its errors are shown for the right file | Always | Required | Application's job |
| UPL-13 | Files are submitted with the form, and the selection is handled after a failed submit | Upload on submit | Required | Application's job |
| UPL-14 | Network loss and leaving the page during an upload are handled | Immediate upload | If applicable | Application's job |
| UPL-15 | Name, hints, status announcements and drop area keyboard access are exposed | Always | Required | Application's job |
| UPL-16 | Camera and gallery sources and large files work on mobile devices | Mobile use | If applicable | Application's job |

## 7. Anti-patterns

- A drop area that cannot be reached by keyboard and has no button.
- Checking the type only by file extension, or only on the client.
- A removed file that cannot be selected again.
- Progress with no text alternative.
- A failed upload that discards the files that succeeded.
- A form that silently loses the chosen files after a validation error.
- Showing the full path or a raw error from the server.

## 8. Test cases

| ID | Category | Applies when | Capability | Test (generic) | Expected result | Obligation | Verification | Priority |
|---|---|---|---|---|---|---|---|---|
| UPL-01 | Keyboard | Always | Choose files | Open the selection by pointer and by keyboard | File selection opens, chosen files appear | Required | Automatable | Critical |
| UPL-02 | Functional | Drag and drop | Drop target | Drag a file over and drop it, then do it without dragging | Feedback shown, same result both ways | If applicable | Automatable | Important |
| UPL-03 | Validation | Always | Type and size limits | Choose a file of a wrong type and one too large | Specific message for each, others unaffected | Required | Automatable | Critical |
| UPL-04 | Functional | Multiple files | File list | Add several files, remove one, exceed the count limit | List correct, limit enforced and explained | If applicable | Automatable | Important |
| UPL-05 | States | Immediate upload | Progress | Upload a large file | Progress shown and announced | If applicable | Automatable | Important |
| UPL-06 | Functional | Immediate upload | Cancel | Cancel mid-upload | Stops, status updated, nothing stored | If applicable | Automatable | Important |
| UPL-07 | Functional | Multiple files | Retry | Make one of several uploads fail, retry it | Others kept, retry succeeds | If applicable | Automatable | Critical |
| UPL-08 | Functional | Always | Reselect | Remove a file and choose the same one again | It is accepted, duplicates handled as decided | Required | Automatable | Important |
| UPL-09 | Data | Always | Unusual files | Use an empty file, a huge file, a very long unicode name, no extension, a renamed file of another type | Each handled with clear feedback | Required | Automatable | Critical |
| UPL-10 | Functional | Previews | Previews | Add and remove images | Preview shown and released | Optional | Manual | Nice-to-have |
| UPL-11 | Data | Editing existing data | Stored files | Open an item with existing files, replace and remove one | Shown, changes applied | If applicable | Automatable | Important |
| UPL-12 | Validation | Always | Server validation | Send a file that passes the client check but fails on the server | Error shown for that file | Required | Automatable | Critical |
| UPL-13 | Data | Upload on submit | Form integration | Choose files, fail validation, submit again | Files kept or the user clearly asked to choose again | Required | Automatable | Critical |
| UPL-14 | Functional | Immediate upload | Network loss | Drop the connection mid-upload, leave the page | Failure shown, leaving warned | If applicable | Automatable | Important |
| UPL-15 | Accessibility | Always | Exposed state | Use a screen reader through a full upload | Name, hints and each status announced | Required | Manual | Critical |
| UPL-16 | Functional | Mobile use | Mobile | Choose from camera and gallery, use a large file | Works, no freeze | If applicable | Manual | Important |

Categories: functional, keyboard, states, validation, layout, accessibility, data.
Verification: automatable, manual (screen reader, real mobile device).
Priority: critical, important, nice-to-have.

## 9. Definition of done

- [ ] Every Required capability is built and has a passing test
- [ ] Every applicable If applicable capability is built and tested, or marked not applicable with a reason
- [ ] All Critical test cases pass
- [ ] Manual checks completed or explicitly deferred
- [ ] Accessibility skill checklist applied
