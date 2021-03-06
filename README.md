# Rhea

[![](https://dl.dropboxusercontent.com/s/ic4r48xv2ru5r3l/4ba5c0bcdbdf7d79eb87a72f42f16f72-12wH.jpg?dl=0)](https://en.wikipedia.org/wiki/Rhea_(moon))

Rhea is a status bar utility for the Mac that allows you to quickly and easily upload files and shorten links, similar to [CloudApp](https://www.getcloudapp.com/) and [Dropshare](https://getdropsha.re/). It uses [Dropbox](https://www.dropbox.com/developers) (powered by [TJDropbox](https://github.com/timonus/TJDropbox)) for file storage and the [Bitly](https://dev.bitly.com) or the [Google URL shortener](https://developers.google.com/url-shortener/) for shortening links.

## File Upload

You can drag files into the status bar to upload them to Rhea.

![](https://dl.dropboxusercontent.com/s/g9drnbw4rpr9ytt/1-vC9R.gif?dl=0)

Or, if you have a file path or file URL copied to your clipboard you can upload it via Rhea’s dropdown menu.

![](https://dl.dropboxusercontent.com/s/ae44aa9z4p9a3ig/2-bxlw.gif?dl=0)

Dropbox short links (db.tt) are copied to the clipboard while files are being uploaded in the background, so it’s very quick.

### Technical Notes
- The API one uses to copy a short link while an upload is occurring is deprecated by Dropbox. May have to move to another endpoint at some point.
- A 4-character base 62 suffix is appended to all uploaded files to avoid filename conflicts. This suffix is consistent for a given file's contents, so repeat uploads of the same file with the same filename act as no-ops.
- It is recommended that you use Dropbox’s [selective sync](https://www.dropbox.com/en/help/175) feature to disable the Rhea directory from being synched to your Mac.

## Link Shortening

You can drag links into the status bar to shorten them.

![](https://dl.dropboxusercontent.com/s/8sgrwkzcnib5isl/3-JqyP.gif?dl=0)

Or, if you have a URL copied to your clipboard you can shorten it via Rhea’s dropdown menu.

![](https://dl.dropboxusercontent.com/s/yo2brd16yl7q91k/4-6ql9.gif?dl=0)

### Technical Notes
- I initially chose to use the Google URL shortener because it doesn’t require authentication, whereas Bitly does. I now support Bitly shortening optionally, but when the Google URL shortener is [deprecated in 2019](https://bit.ly/2uVWTC9) this'll become the default.

## Development

- Rhea is open source, however Dropbox, Bitly, and Google API keys aren’t present in the open source repo. In order to develop Rhea you’ll need to provide these keys by doing the following:
	- Fill in `_dropboxAppKey` and add a URL scheme with the format `db-yourDropboxAppKey` to your info.plist's entry for `CFBundleURLTypes` for Dropbox auth.
	- Fill in `_bitlyClientIdentifier`, `_bitlyClientSecret`, and add `rhea-bitly-auth://bitlyauth` as a whitelisted redirect URI in your Bitly app's OAuth app settings for Bitly auth.
	- Fill in `kRHEAGoogleKey` to use the Google URL shortener.
- Rhea uses [git submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules), so run `git submodule update --init` when cloning.