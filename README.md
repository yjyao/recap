# Recap --- Review what you've learned based on the [forgetting curve](http://enwp.org/forgetting_curve).

`Recap` is a CLI tool that lists items from your personal notes for you to
review, based on a user-defined review schedule.

The forgetting curve is a model hypothesized by Hermann Ebbinghaus, depicting how much more information one memorizes with periodical reviews than without.

## Installation

Clone the repository

```sh
$ git clone http://github.com/yjyao/recap
```

and run it with `/path/to/repo/recap`, or create a symbolic link for it under
`~/bin`, or ~/.local/bin`, or wherever your `$PATH` can see.

```sh
$ ln -s /path/to/repo/recap ~/.local/bin/
```

## Usage

To use the tool, you need to create notes first. The tool looks for the
following files as its data source, in the order listed: `./notes.recap`,
`~/.notes.recap`, `~/.recap/notes.recap`. It is recommended that you create a
`~/.recap/notes.recap`. If you'd like to store the notes somewhere else, set `RECAP_NOTES_PATH` (for example in `~/.bashrc`).

The default recap schedules are found in `schedule.txt`. You can create
`~/.recap/schedule.txt` or set `RECAP_SCHED_PATH` to override it. The default
schedules define progressively larger intervals, at approximately one day after
you've put the note, half a week after, a week after, a month after, three
months after, half a year after, and a year after, in total seven rounds.

With `notes.recap` and `schedules.txt` available, run

```sh
$ recap
```

to print a list of items you should review today.

## Notes syntax

Each line is a note. The line must start with a date indicating when you
learned the knowledge. The date must be in [ISO 8601
format](http://enwp.org/iso_8601), for example `2012-12-21`. The rest of the
line is the content of the note.

Optionally, a note can contain projects/themes denoted with a plus sign
prefixed to the project name, for example `+my-project`. This notation is
stolen from [todo.txt](https://github.com/todotxt/todo.txt) and has no effects
on the tool (the tool will not recognize or do anything with the project tags).

A note can also contain hidden text for self-examination purposes. This can be
useful for study notes like answers to a question (think of flash cards).
Hidden text is surrounded with a pair of curly braces.

Here is an example note:

```
2020-02-02 hola {hello} +spanish
```

When passed with `--hidden`, the tool replaces hidden text with an sterisk
(`*`).

## Schedule syntax

Each line is a positive whole number, indicating how many days after a note is
taken should the note be reviewed. With a `schedule.txt`

```
1
3
10
```

for the note

```
2020-02-02 mt fuji is (partially) privately owned land
```

the tool will list this item when you run it on the day after the date
(2020-02-03), the third day after (2020-02-05), and the tenth day after
(2020-02-12).
