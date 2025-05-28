# CivitAI model downloader

This project is a personalized and enhanced fork of the original Civitai Downloader by [ashleykleynhans](https://github.com/ashleykleynhans), available at [https://github.com/ashleykleynhans/civitai-downloader](https://github.com/ashleykleynhans/civitai-downloader).

The original project appears to be no longer actively maintained. This version incorporates substantial modifications and new features tailored for my personal use.

## Key Changes & Enhancements in This Version

* Uses `requests` instead of `urllib3` for CivitAI API calls
* Adds support for batch downloading
* Adds support for using AIR (Artificial Intelligence Resource) in addition to URL
* Major Refactor of Core Logic: `download.py` has been significantly reworked for readability, sanitized filenames, and some QoL improvements like a progress bar.

## Getting Started

This script requires a [CivitAI](https://civitai.com/user/account)
API key.  You can create the API key as follows:

1. Log into [CivitAI](https://civitai.com).
2. Go to the [Manage Account](https://civitai.com/user/account) page.
3. Scroll down to the `API Keys` section, close to the bottom of the page.
4. Click the `+ Add API key` button to create a new API key.
5. Give the API key a name and click the `Save` button.
6. You will then use your newly created API key with this script.

## Installation

```bash
git clone https://github.com/iresprite/civitai-downloader.git
cd civitai-downloader/
pip install .
```

> [!IMPORTANT]
> It is important to ensure that you use either the **DOWNLOAD** link
> (not the link to the model page in CivitAI) or the AIR ([Artificial Intelligence Resource](https://github.com/civitai/civitai/wiki/AIR-%E2%80%90-Uniform-Resource-Names-for-AI)). You can find the download link by right-clicking the Download button (or the file you want to download), and hitting Copy Link. 

## Usage

To use civitai-dl, you'll specify either a model URL or an AIR identifier, along with a local directory to save the files. You can also customize the download with various options.

### Basic Command Structure

```bash
civitai-dl [TARGET] [OPTIONS] --local-dir /path/to/your/download/directory
```

### Required Arguments
To run civitai-dl, you must provide the following arguments.
1. **Target Specification (Choose one):**
   - `--url <URL_1> [URL_2 ...]`
       - Use this to download models directly using their Civitai API download URL(s).
       You can provide one or more URLs.
   - `--air <AIR_1> [AIR_2 ...]`
2. **A Destination Directory:**
   - Use this to download models using their Civitai AIR identifier(s) (e.g., urn:air:civitai:12345@version:67890).
       You can provide one or more AIRs.
   - `--local-dir <DIRECTORY_PATH>`
   - Specifies the local directory where models and associated files will be saved. This argument is always required.

### Common Options:
- `--size {full,pruned}`- Specify the desired model size.
    - full: Download the full model file.
    - pruned: Download the pruned version of the model, if available.
- `--fp {8,16,32}`
  - Specify the desired floating-point precision for the model, if different versions are available. 
  - 8: FP8 
  - 16: FP16 (often a good balance of size and quality)
  - 32: FP32 (full precision)
- `--include-companions`
  - Download any companion files (e.g., VAEs, textual inversions) associated with the main model. 
- `--token <YOUR_CIVITAI_API_TOKEN>`
  - Your personal Civitai API key. Recommended for accessing your account details or potentially higher rate limits.
- `--force-unsafe`
  - By default, the script might try to avoid downloading files marked as potentially unsafe or unverified by Civitai. This flag bypasses such checks. Use with caution.
- `--debug`
  - Enable debug logging for more verbose output, which can be helpful for troubleshooting.
- `-h, --help`
  - Show the full help message with all available options and exit.

### Examples
1. **Download a model using its URL to the current directory:

```bash
civitai-dl --url https://civitai.com/api/download/models/12345 --local-dir .
```

2. **Download multiple models using their AIR identifiers to a specific directory:**

```bash
civitai-dl --air urn:air:civitai:12345@version:67890 \
    urn:air:civitai:23456@version:78901 \
    --local-dir /mnt/storage/civitai_models
```
3. **Download a pruned, FP16 version of a model, including companions, using an API token:**

```bash
civitai-dl --url https://civitai.com/api/download/models/12345 \
            --size pruned \
            --fp 16 \
            --include-companions \
            --token YOUR_API_TOKEN_HERE \
            --local-dir ./downloaded_model
```

4. **Download a model using its AIR, forcing unsafe download if necessary:**

```bash
civitai-dl --air urn:air:civitai:34567@version:89012 \
            --force-unsafe \
            --local-dir ./unsafe_downloads
```

## License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.