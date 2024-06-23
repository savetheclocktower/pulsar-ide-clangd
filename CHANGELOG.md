# 0.6.3 — 2024-06-23

* Bump `@savetheclocktower/atom-languageclient` to
  * add support for reporting server-initiated progress messages on async tasks when `busy-signal` is installed;
  * fix bugs relating to the `refactor` service and server capabilities in general.
* Provide only the “enhanced” version 0.2.0 of the `refactor` service, since `clangd` supports `prepareRename` requests.
  * This means that `clangd` will be able to tell us what the renameable token is (if any) at the cursor.
