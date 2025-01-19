# Obsidian Zip

**Obsidian Zip** is a Rust library designed to aid in managing and archiving directories into zip files. It is part of the larger Obsidian Minecraft Server Portal project and serves as a utility for handling zip files efficiently. This library leverages parallel processing for improved performance and is designed to be added as a **Git dependency** in your Cargo.toml.

## Features

- Traverse directories recursively using [walkdir](https://docs.rs/walkdir).
- Create zip archives with configurable compression via [zip](https://docs.rs/zip).
- Leverage [rayon](https://docs.rs/rayon) for multithreaded file processing to maximize performance.
- Define custom file filters to include or exclude specific files and directories.
- Friendly error handling with a robust custom error type.

## Requirements

- **Rust**: Version `1.82.0` or later is recommended.
- This library is only available as a Git dependency.

## Installation

To use this library in your project, add it as a Git dependency in your `Cargo.toml`:

```toml
[dependencies]
obsidian-zip = { git = "https://github.com/Obsidian-Minecraft-Server-Portal/zip.git", branch = "main" }
```

## Usage

The library provides functionality to archive a directory into a zip file with a simple API. Below is an example of how to use it:

### Example

```rust
use obsidian_zip::archive_directory;
use std::path::Path;

fn main() -> Result<(), obsidian_zip::ArchiveError> {
    // Paths to the target directory and the output file.
    let directory = Path::new("/path/to/directory");
    let output_file = Path::new("/path/to/output.zip");

    // Apply a filter to exclude specific files (e.g., temporary files).
    archive_directory(directory, output_file, &|path| {
        !path.extension().map_or(false, |ext| ext == "tmp")
    })?;

    Ok(())
}
```

In this example:
- Replace `/path/to/directory` with the path to the directory you want to zip.
- Replace `/path/to/output.zip` with the desired output file name.
- The filter excludes files with a `.tmp` extension.

### Error Handling

The library uses a custom error type, `ArchiveError`, to capture and propagate errors throughout the operations, such as:
- I/O errors
- Zip creation errors
- Directory traversal errors

## Features Used

This library uses the following dependencies:
- **[walkdir](https://docs.rs/walkdir)**: For recursive directory traversal.
- **[zip](https://docs.rs/zip)**: For handling zip files and compression.
- **[rayon](https://docs.rs/rayon)**: For parallel file processing to speed up file reading.
- **[log](https://docs.rs/log)**: For future logging capability.

## License

This project is licensed under the **LGPL-3.0 License**. See the [LICENSE](https://www.gnu.org/licenses/lgpl-3.0.html) file for more details.

## Contributing

Contributions to the library are welcome! If you find a bug, have a feature request, or want to contribute improvements, feel free to create an issue or submit a pull request in the [GitHub repository](https://github.com/Obsidian-Minecraft-Server-Portal/zip.git).

---

*Obsidian Zip* is a robust and efficient tool for managing zip archives, specifically designed to power the Obsidian Server Portal. Thank you for using our library!