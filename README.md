## procedure

1. `corepack enable`
2. `pnpm rm @webext-core/messaging`
  - Clean lockfile(reproduce initialization)
4. `pnpm add @webext-core/messaging`
  - Added only info about the `@webext-core/messaging` in lockfile
  - ```
    snapshots:

      '@webext-core/messaging@2.0.1': {}
    ```
5. `pnpm add @webext-core/messaging` (Add again)
  - Added more info about dependencies in lockfile
  - part of e.g.
    - ```
      .
      .
      .
      snapshots:

        '@lukeed/csprng@1.1.0': {}

        '@webext-core/messaging@2.0.1':
          dependencies:
            serialize-error: 11.0.3
            uid: 2.0.2
            webextension-polyfill: 0.10.0
      .
      .
      .
      ```
6. `pnpm dedupe --check`
  - Duplicates found, suggesting first-time installation status
  - ```
    ERR_PNPM_DEDUPE_CHECK_ISSUES  Dedupe --check found changes to the lockfile

    Packages
    @webext-core/messaging@2.0.1
    ├── - serialize-error 11.0.3
    ├── - uid 2.0.2
    └── - webextension-polyfill 0.10.0
    
    - @lukeed/csprng@1.1.0
    - serialize-error@11.0.3
    - type-fest@2.19.0
    - uid@2.0.2
    - webextension-polyfill@0.10.0
    
    Run pnpm dedupe to apply the changes above.
    ```
7. `pnpm dedupe`
  - Return to status 4(first-time installation lockfile)
8. `pnpm i --fix-lockfile`
  - Return to status 5 (second-time installation lockfile)


## screenshots

![image](https://github.com/user-attachments/assets/b7d7328b-8502-4574-8de7-c3c685a32083)

![image](https://github.com/user-attachments/assets/99981503-de59-4db0-b20f-829274cb88f7)

![image](https://github.com/user-attachments/assets/ef9797ed-a3de-447c-a4bd-83f2821230f3)
