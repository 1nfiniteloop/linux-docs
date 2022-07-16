# category: compression & decompression

## Tools

* `tar` - tape-archive, which bundles and compress files (not by
  default).
* `gzip`, `gunzip` - Compress file using using Lempel-Ziv coding (LZ77).
* `bzip2`, `bunzip2` - Compress file using bzip2 algorithm, generally
  better than conventional LZ77/LZ78-based.
* `zip`, `unzip` - A compression and file packaging utility, supported by many
  systems and platforms.
* `cpio` - This format is mainly used for initramfs.
* `ar` - Mainly used to compress object-files (.o) into an ar-file (.a),
  when compiling static libs.

## Files

_None_

## Usage

### tar

Common used flags for `tar`:

* `[-t|--list]`
* `[-x|--extract]`
* `[-z|--gzip|--gunzip]`
* `[-f|--file]`
* `[-O|--to-stdout]`
* `[-C|--directory]`

#### Extract

* From file: `tar -xzf ${archive_name}`
* From stdin: `cat ${archive_name} |tar -xz`
* To stdout: `tar --to-stdout -xzf ${archive_name}`

#### Compress

* From file: `tar -czf ${archive_name} [file, [file, ...]]`
* From stdin: _Not applicable_.
* To stdout: `tar -cz ${archive_name} > ${archive_name}.tar.gz`

### gzip, gunzip

Common used flags for `gzip` and `gunzip`:

* `[-d|--decompress]`
* `[-c|--stdout|--to-stdout]`

#### Extract

* From file: `gunzip ${archive_name}`
* From stdin: `cat ${archive_name} |gunzip > ${archive_name%.gz}`
* To stdout: `gunzip -c ${archive_name} > ${archive_name%.gz}`

#### Compress

* From file: `gzip ${archive_name}`
* From stdin: `cat ${file_name} |gzip > ${file_name}.gz`
* To stdout: `gzip -c ${file_name} > ${file_name}.gz`

### zip

Common used flags for `zip` and `unzip`:

* `[-l]` list files (for `unzip` only)
* `[-q|--quiet]`

#### Extract

* From file: `unzip ${archive_name}`
* From stdin: _Not applicable_, but `cat ${archive_name} |unzip -` might work
  dependent on implementation.
* To stdout: _Not applicable_.

#### Compress

* From file: `zip ${archive_name} [file, [file, ...]]`
* From stdin: _Not applicable_, but can take filenames from stdin with
  `echo "first.txt" |zip -@`.
* To stdout: _Not applicable_.

### cpio

Uncompress initramfs, which is a gzip compressed cpio archive:
`gunzip --stdout initramfs |cpio --extract`.
