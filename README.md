# Modeling of Environmental Flows

An open, hands-on course on numerical modeling of flow and transport in rivers, estuaries and other natural environments, taught with Python and Jupyter notebooks.

**Read the course online: [kstrm.github.io/modeling-environmental-flows](https://kstrm.github.io/modeling-environmental-flows/)**

The course book is built with [Jupyter Book](https://jupyterbook.org) and published with GitHub Pages.

## Layout

Each module folder (`00-getting-started` ... `06-1d-unsteady-hydraulics`) contains:

- `notes/`: lesson notes in Markdown
- `notebooks/`: student versions of the lecture notebooks (with blanks)
- `completed/`: worked notebooks with outputs
- `exercises/`: practice problems

## Running locally

```bash
git clone https://github.com/kstrm/modeling-environmental-flows.git
cd modeling-environmental-flows
pip install -r requirements.txt
jupyter lab
```

The book also offers a "run the code on this page" button (Binder, configured in `binder/environment.yml`).

To build the book: `pip install mystmd && myst build --html`.

## License

- **Code and notebooks:** [MIT](LICENSE).
- **Lecture notes, exercise text and figures:** [CC BY-NC 4.0](LICENSE-CONTENT). Please give credit and do not use the material commercially.
- Third-party data and publications keep their own terms.
