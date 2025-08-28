<Instructions>
- You are to follow the instruction below precisely to create a solution that meets the objective.
- The context section will list the files you can edit, the programming language to use, and any other key constraints.
- The <tasks> will give information on the activities to undertake. 
- If there any custom instructions these will be described in blocks
</Instructions>


<Name>
   Command-Line EPUB to PDF Conversion Utility in Python
</Name>

<Objective>
- The desired outcome is a high-quality, performant, and robust command-line utility written in Python that converts EPUB files into PDF documents.
- Success is defined as a tool that can be executed from the command line, accepts specific parameters for input and output, handles errors gracefully, and produces a PDF that is a visually accurate representation of the source EPUB file, preserving layout, images, and text formatting.
- Key features required are:
    - Command-line argument parsing for an input EPUB file, an output PDF file path, and a processing mode (test/live).
    - Robust error checking for file paths, file formats, and the conversion process.
    - A "test" mode that validates inputs and prerequisites without creating a file.
    - A "live" mode that performs the full conversion and saves the PDF.
    - High fidelity in the conversion, ensuring the PDF accurately reflects the EPUB's content and styling.
- This utility must be a command-line interface (CLI) application. Any form of graphical user interface (GUI) is explicitly excluded.
</Objective>

<Context>
- A new file will need to be created: `epub_converter.py`.
- The programming language to be used is Python 3.
- The solution should be "Python native," meaning it should rely on standard Python libraries and third-party packages that can be installed via pip. It should avoid dependencies on external applications that need to be installed and managed separately from the Python environment.
- The application must be performant, capable of handling reasonably sized EPUB files without excessive memory consumption or processing time.
</Context>

<Tasks>

1. **Task 1: Implement Command-Line Argument Parser**
   - Utilize Python's `argparse` module to create a command-line interface.
   - The interface must accept three arguments:
     - `input_pub`: The path to the source EPUB file. This should be a required positional argument.
     - `--output` or `-o`: An optional argument to specify the path and filename for the output PDF. If not provided, the output PDF should be created in the same directory as the input file, with the same base name but a `.pdf` extension.
     - `--mode`: An optional argument that accepts two values: 'live' or 'test'. The default value should be 'live'.

2. **Task 2: Develop EPUB File Ingestion and Validation**
   - Implement logic to validate the path provided for the input EPUB file, ensuring it exists and is accessible.
   - Add robust error checking to verify that the input file is a valid EPUB file. This could involve checking the file's magic number or attempting to parse its core structure (e.g., the `META-INF/container.xml` file).
   - Gracefully handle and report errors if the file is not found, is not a valid EPUB, or is corrupted.

3. **Task 3: Core EPUB to PDF Conversion Logic**
   - Implement the primary functionality to parse the EPUB's content. This involves programmatically unzipping the EPUB container, reading the OPF package file to determine the reading order of the content documents (XHTML files), and identifying the associated CSS stylesheets.
   - Integrate a suitable Python library to render the sequence of XHTML and CSS content into a single, cohesive PDF document.
   - Ensure that images embedded within the EPUB are correctly processed and included in the final PDF.
   - The conversion must maintain a high degree of fidelity, preserving the original text formatting, layout, and styles as defined in the EPUB's CSS.

4. **Task 4: Implement Test and Live Modes**
   - The application's behavior should change based on the `--mode` flag.
   - In 'live' mode (default), the script will execute the full conversion process and write the final PDF to the specified output path.
   - In 'test' mode, the script should perform all initial validation steps (checking the input file, parsing the EPUB structure) and report that all checks have passed successfully, but it must stop before the final PDF generation and file writing step. It should output a message indicating that "Test mode successful. No file was created."

5. **Task 5: Implement Comprehensive Error Handling and Logging**
   - Integrate `try...except` blocks throughout the code to manage potential runtime errors, including file I/O errors (e.g., permission denied when writing the output file), library-specific conversion errors, and issues with parsing malformed EPUB content.
   - Provide clear, user-friendly feedback to the console. On success, it should print a confirmation message with the path to the created PDF. On failure, it should print a descriptive error message explaining what went wrong, allowing the user to diagnose the problem.

*(End of tasks)*
</Tasks>


<Blocks>

</Blocks>