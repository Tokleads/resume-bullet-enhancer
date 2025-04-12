# resume-bullet-enhancer
# From app.py - Core Enhancement Logic
def enhance_single_bullet(bullet):
    """Enhance a single bullet point with action verbs and quantifiers."""
    # Clean the bullet
    bullet = bullet.strip()
    if not bullet:
        return ""
    
    # Extract key content words
    words = re.findall(r'\b\w+\b', bullet.lower())
    
    # Determine the best verb category based on content
    category = determine_verb_category(words)
    
    # Select a random action verb from the appropriate category
    action_verb = random.choice(ACTION_VERBS[category])
    
    # Add a quantifier with a random number
    number = random.randint(10, 95)
    quantifier = random.choice(QUANTIFIER_PATTERNS).format(number=number)
    
    # Basic content extraction (simple approach)
    original_content = re.sub(r'^(managed|created|developed|worked|helped|made|did|used|performed|handled|supported|assisted|conducted|prepared|provided|generated|maintained|built|wrote|designed)\s+', '', bullet, flags=re.IGNORECASE)
    
    # Enhance with specific action and quantifier
    enhanced = f"{action_verb} {original_content} {quantifier}"
    
    return enhanced
    // From static/script.js - Processing API Results
function displayResults(data) {
    resultsContent.innerHTML = '';
    
    if (!data.enhanced_bullet_points || data.enhanced_bullet_points.length === 0) {
        showError('No enhanced bullet points were generated.');
        return;
    }
    
    // Create a table to display the results
    const table = document.createElement('table');
    table.className = 'table table-striped';
    
    // Create table header
    const thead = document.createElement('thead');
    const headerRow = document.createElement('tr');
    headerRow.innerHTML = `
        <th style="width: 45%">Original</th>
        <th style="width: 45%">Enhanced</th>
        <th style="width: 10%">Actions</th>
    `;
    thead.appendChild(headerRow);
    table.appendChild(thead);
    
    // Create table body
    const tbody = document.createElement('tbody');
    
    data.enhanced_bullet_points.forEach((item, index) => {
        // Table row creation...
        
        // Add cells to the row
        row.appendChild(originalCell);
        row.appendChild(enhancedCell);
        row.appendChild(actionsCell);
        
        // Add the row to the table body
        tbody.appendChild(row);
    });
    
    table.appendChild(tbody);
    resultsContent.appendChild(table);
    resultsContainer.classList.remove('d-none');
}
<!-- From templates/index.html - Main Form Section -->
<div class="card mb-4">
    <div class="card-header">
        <h2>Input Your Resume Bullet Points</h2>
    </div>
    <div class="card-body">
        <form id="enhancer-form">
            <div class="mb-3">
                <label for="bullet-points" class="form-label">Enter one or more bullet points (one per line):</label>
                <textarea 
                    class="form-control" 
                    id="bullet-points" 
                    rows="6" 
                    placeholder="Example: 
Managed a team of developers 
Created reports for stakeholders
Developed new features for the application"
                ></textarea>
            </div>
            <div class="d-grid gap-2">
                <button type="submit" class="btn btn-primary" id="enhance-button">
                    <i class="fas fa-magic me-2"></i>Enhance Bullet Points
                </button>
            </div>
        </form>
    </div>
</div>
/* From static/style.css - Styling for Cards and Animation */
.card {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: none;
    transition: transform 0.2s, box-shadow 0.2s;
}

.card:hover {
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
}

/* Animations */
@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

#results-container:not(.d-none) {
    animation: fadeIn 0.5s ease-in-out;
}
# From app.py - Categorized Action Verbs
ACTION_VERBS = {
    "leadership": [
        "Directed", "Orchestrated", "Spearheaded", "Led", "Championed", 
        "Managed", "Guided", "Supervised", "Administered", "Coordinated"
    ],
    "achievement": [
        "Achieved", "Exceeded", "Improved", "Pioneered", "Transformed",
        "Boosted", "Delivered", "Accelerated", "Optimized", "Enhanced"
    ],
    "technical": [
        "Implemented", "Programmed", "Engineered", "Designed", "Developed",
        "Architected", "Coded", "Configured", "Deployed", "Integrated"
    ],
    "communication": [
        "Negotiated", "Persuaded", "Presented", "Collaborated", "Facilitated",
        "Communicated", "Consulted", "Advised", "Authored", "Promoted"
    ],
    "analytical": [
        "Analyzed", "Evaluated", "Researched", "Identified", "Calculated",
        "Assessed", "Diagnosed", "Examined", "Investigated", "Surveyed"
    ]
}
