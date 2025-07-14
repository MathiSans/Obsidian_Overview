<%*
const folderPaths = ["3_ARCHIVE"]; // Folders to check for existing IDs

// Function to retrieve all existing IDs from the frontmatter of target folders
function getExistingIds(folders) {
    const files = app.vault.getMarkdownFiles();
    const ids = [];

    for (const file of files) {
        if (folders.some(folder => file.path.startsWith(folder))) {
            const frontmatter = app.metadataCache.getFileCache(file)?.frontmatter;
            if (frontmatter && frontmatter["id"]) {
                ids.push(frontmatter["id"]);
            }
        }
    }
    return ids;
}

// Function to generate a random 6-digit HEX ID
function generateRandomId(existingIds) {
    let id;
    do {
        id = Math.floor(Math.random() * 0x1000000).toString(16).padStart(6, '0').toUpperCase();
    } while (existingIds.includes(id)); // Ensure uniqueness
    return id;
}

// Fetch all existing IDs
const existingIds = getExistingIds(folderPaths);

// Generate a new unique ID
const uniqueId = generateRandomId(existingIds);
-%>
"<%* tR += uniqueId %>"