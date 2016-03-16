 # overview
Describe the outline of the in-queue worker

## workflow
An in-queue worker is created by a process-unit and assigned tasks from it as well.
(*perhaps in-queue works are in a pool and waiting for new tasks coming?*)

In-queue workers iterates users in the sub tasks then save messages into indepent queues for each users.
