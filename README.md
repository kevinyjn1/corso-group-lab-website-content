# Corso Group website: the content

This repository holds the words and lists of the Corso Group website: its papers, people, talks,
releases, courses, and research areas. Each entry is one small text file. The website's design and
code live in [another repository](https://github.com/kevinyjn1/corso-group-lab-website).

When anything here changes, the website is rebuilt and published by itself, usually within three
minutes.

## Editing the website

You do not need to know anything on this page to edit the site. Open the editor, change a form,
and save:

**<https://app.pagescms.org/kevinyjn1/corso-group-lab-website-content>**

- **Signing in.** The website's manager invites you by email. Open the editor, enter that email
  address, and type in the six-digit code it sends you. No password, no GitHub account.
- **Adding something.** Choose a list on the left (Publications, People, Talks, press, and essays,
  Code and data, Courses), start a new entry, fill in the form, and save. Boxes that do not
  apply can stay empty.
- **Changing something.** Find the entry with the search box, open it, change it, and save.
- **When someone graduates or leaves.** Open their entry under People, change "In the group now?"
  to Alumni, and fill in the year. Do not delete them: alumni are listed on the site.
- **Seeing it live.** Give it three minutes, then reload the website.

### What to write

The site speaks for a research group, and a wrong fact on it is worse than a missing one.

- State only what a public source says in so many words: the paper, the venue's page, the
  person's own page. Titles, awards, dates, counts, and the word "first" are the usual mistakes.
- Use the item's own title, and the link to the item itself, with nothing after a "?" that tracks
  who shared it.
- Nothing unpublished: no results under review, no internal numbers, no slides that are not public.
- Everything saved here is public at once and stays in the history, so never paste anything
  private.

### If a change does not appear

Before anything is published it is checked. A change that fails a check is not published, and the
website stays as it was. The usual causes are a link that does not start with `https://` and a
required box left empty.

When that happens, a note titled "A change to the website could not be published" appears under
[Issues](https://github.com/kevinyjn1/corso-group-lab-website-content/issues) and says which entry
and which box. Fix the entry in the editor and save it again. The note closes by itself once a
publish goes through.

## Managing the website

One person, the manager, looks after access and the rare thing that needs a decision. It takes a
GitHub account with write access to this repository. It does not take programming.

| To do this | Do this |
| --- | --- |
| Let someone edit | In the editor, open **Collaborators** and add their email address. Use their university address. |
| Stop someone editing | Remove them from **Collaborators**. It takes effect at once. |
| Undo a change | On GitHub, open **Commits**, find the change (each one names who made it), open it, and choose **Revert**. That publishes the earlier version again. |
| Publish again by hand | Open **Actions**, choose **Publish**, and press **Run workflow**. Do this after the website's code has changed, or wait for the nightly run. |
| See why a publish failed | Open **Issues**, or the failed run under **Actions**. |
| Cut the editor off entirely | In GitHub's **Settings**, **GitHub Apps**, suspend or uninstall "Pages CMS". Entries can still be edited as files on GitHub. |

To be told when a publish fails, press **Watch** on this repository and choose **All Activity**.

### If the editor shows the forms but will not save

A red message that says "Resource not accessible by integration" comes from GitHub, not from the
form: the editor's app has no right to write to this repository. Signing in to the editor is not
enough, and the forms still appear because this repository is public. On GitHub, open
**Settings**, **Applications**, **Pages CMS**, **Configure**, choose **Only select repositories**,
select this repository and no other, and save. Then reload the editor and save again.

### Handing the site to the next manager

The site should belong to an organization the professor owns, with two owners, so that it never
depends on one student's account. To hand over, an owner adds the new manager to the organization
with write access to both repositories and removes the old one. Nothing else moves.

If the repositories themselves are ever moved to another owner, three things need doing:

1. Change `CODE_REPOSITORY` in `.github/workflows/publish.yml` to the code repository's new name,
   and the links in this file.
2. Install Pages CMS on this repository under the new owner ("Only select repositories", this one
   only), and invite the editors again.
3. Publish once by hand. The website's address changes with the owner unless a university name
   already points to it.

## How it is kept safe

The editor is an outside service. It can write to this repository and to nothing else: it is not
installed on the code repository at all. So this repository is treated as untrusted, and the
checks are made by the code, which the editor cannot reach.

On every publish, in `.github/workflows/publish.yml`:

1. **The content gate** (in the code repository, `scripts/content-gate.mjs`) reads this repository
   and copies only what it recognizes: the six folders, plain `.yaml` files with simple names, each
   holding one entry of a sane size. Everything else is left behind, including this file and the
   editor's settings. Nothing here is ever run as a program.
2. **The content rules** (`src/content.config.ts`) check every box of every entry: text where text
   belongs, a number where a number belongs, a choice from the list, and links that are ordinary
   web addresses. A box the site does not know is refused.
3. **The site is built and every page is tested**: it loads without an error, shows its pictures,
   fits the screen, links only to real places, and runs no code but the site's own.

Only then is it published, and only from the `main` branch. The worst an intruder with an editor's
access could do is change words and links, which the history shows and one click undoes.

`.pages.yml` describes the editor's forms. It makes editing pleasant; it is not a safeguard. The
three checks above are, and they do not read it.

## The files

| Folder | One file per | Notes |
| --- | --- | --- |
| `publications/` | paper | |
| `people/` | person | current members and alumni |
| `media/` | talk, podcast, article, or essay | |
| `resources/` | dataset or software release | |
| `courses/` | course | |
| `areas/` | research area | a fixed set of six; their text can change |

A file's name, without `.yaml`, is the entry's address on the site (for example
`#li2026mistake` on the Publications page), so files are not renamed once they exist.
