2020-12-26, Intro to CSS, 15:30

Cascading Stylesheets
• Not a programming language
• Styling language
• Website layout and design
• Three ways to use CSS
○ Inline: inside the HTML element (DO NOT USE)
○ Internal CSS: using the <style> tags within the .html doc
§ You can reference html tags (h1, p) or custom classes and IDs
○ External CSS: linking external .css file (Recommended to debloat .html)

    • There are web-safe fonts like Arial and Helvetica that can be applied simply by calling them
    	○ Custom fonts would need to be downloaded to the folder structure and loaded on page-load
    • Margins can be negative, or auto.
    • Padding cannot be negative nor auto.

Ways to declares values for a square (content, padding, border, marging): 1. Long way, declaring all four sides
top: 5px;
right: 10px;
bottom: 5px;
left: 10px; 2. Short, declaring all four sides at once
5px 10px 5px 10px; 3. Shorter, declaring three values for top, sides, and bottom
5px, 10px, 7px; 4. Shorterer, declaring top/bottom and right/left
5px 10px; 5. Shortest, declaring all values as one
10px;

Apply to all css files freely
_ {
box-sizing: border-box; /_ to add width and padding to box total width \*/
}
