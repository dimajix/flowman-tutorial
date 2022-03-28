# Lesson 7 - Execution Phases and Lifecycles

### Objectives

* You will learn how to use Flowman Shell to support development
* You will know the most important command of Flowman Shell
* You will understand job contexts and why they are required

### Processing Steps


## Execution Phases
Flowman sees data as artifacts with a common lifecycle, from creation until deletion. The lifecycle itself consists of
multiple different phases, each of them representing one stage of the whole lifecycle.

### Lifecycle Phases
The full lifecycle consists out of specific execution phases, as follows:

1. **VALIDATE**.
   This first phase is used for validation and any error will stop the next steps. A validation step might for example
   check preconditions on data sources which are a hard requirement.

2. **CREATE**.
   This will create all relations (tables and directories) specified as targets. The tables will not contain any data,
   they only provide an empty hull. If a target already exists, a migration will be started instead. This will migrate a
   relation (table or directory) to a new schema, if required. Note that this is not supported by all target types, and
   even if a target supports migration in general, it may not be possible due to unmigratable changes.

3. **BUILD**.
   The *build* phase will actually create all records and fill them into the specified relations.

4. **VERIFY**.
   The *verify* phase will perform simple checks (for example if a specific Hive partition exists), or may also include
   some specific user defined tests that compare data. If verification fails, the build process stops.

5. **TRUNCATE**.
   *Truncate* is the first of two phases responsible for cleanup. *Truncate* will only remove individual partitions from
   tables (i.e. it will delete data), but it will keep tables alive.

6. **DESTROY**.
   The final phase *destroy* is used to physically remove relations including their data. This will also remove table
   definitions, views and directories. It performs the opposite operation than the *create* phase.

Some execution phases can be performed in a meaningful way one after the other. Such a sequence of phases is
called *lifecycle*. Flowman has the following lifecycles built in:

#### Build
The first lifecycle contains the three phases *VALIDATE*, *CREATE*, *BUILD* and *VERIFY*.

#### Truncate
The second lifecycle contains only the single phase *TRUNCATE*

#### Destroy
The last lifecycle contains only the single phase *DESTROY*


## Execution of Phases and Lifecycles

Another lifecycle can be executed by replacing `build` with another execution phase. Flowman will then execute the
lifecycle containing that phase up until this phase. If you want to skip all other execution phases, you can specify
`--no-lifecycle` on the command line.

```shell
flowexec -f <project_dirctory> job <execution_phase> <job_name> [--force] [--no-lifecycle]
```

### Perform full `BUILD` lifecycle

### Perform full `DESTROY` lifecycle

### Perform only `CREATE` phase

### Perform only `BUILD` phase
