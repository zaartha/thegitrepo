# Git Areas — Reference Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    Your Computer                         │
│                                                         │
│  ┌──────────────┐   git add   ┌──────────────┐         │
│  │   Working    │ ──────────► │   Staging    │         │
│  │  Directory   │             │    Area      │         │
│  │              │ ◄────────── │  (Index)     │         │
│  │  (your files)│  git restore│              │         │
│  └──────────────┘             └──────┬───────┘         │
│                                      │ git commit       │
│                                      ▼                  │
│                               ┌──────────────┐         │
│                               │    Local     │         │
│                               │  Repository  │         │
│                               │  (.git dir)  │         │
│                               └──────┬───────┘         │
└──────────────────────────────────────┼─────────────────┘
                                       │ git push
                                       ▼
                               ┌──────────────┐
                               │    Remote    │
                               │  Repository  │
                               │  (GitHub)    │
                               └──────────────┘
```
