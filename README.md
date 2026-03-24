<div align="center">

[![Discord](https://img.shields.io/badge/Discord-7289DA?logo=discord&logoColor=white)](https://discord.gg/fiftyone-community)
[![Hugging Face](https://img.shields.io/badge/Hugging_Face-purple?style=flat&logo=huggingface)](https://huggingface.co/Voxel51)
[![Voxel51 Blog](https://img.shields.io/badge/Voxel51_Blog-ff6d04?style=flat)](https://voxel51.com/blog)
[![Newsletter](https://img.shields.io/badge/Newsletter-BE5B25?logo=mail.ru&logoColor=white)](https://share.hsforms.com/1zpJ60ggaQtOoVeBqIZdaaA2ykyk)
[![LinkedIn](https://img.shields.io/badge/In-white?style=flat&label=Linked&labelColor=blue)](https://www.linkedin.com/company/voxel51)
[![Twitter](https://img.shields.io/badge/Twitter-000000?logo=x&logoColor=white)](https://x.com/voxel51)
[![Medium](https://img.shields.io/badge/Medium-12100E?logo=medium&logoColor=white)](https://medium.com/voxel51)

</div>

Guidelines for the getting started docs
https://github.com/thesteve0/v51-gs-draft/blob/main/GETTING_STARTED_FORMAT.md

1. Make a directory in docs/getting_started/focused_getting_starteds for your project
2. Make juypter notebook in this directory
2. Remember, all images and other files go in an "assets" directory inside project directory 
3. No GIFs. Animated images should be in webp (ideally all images are in webp).
4. Images should not be more than 1600x wide
5. You can do a `mkdocs serve --dirty` and it will render your notebook and you can preview it

**YOU MUST RUN THE BUILD AND SERVE BEFORE DOING A PR - it is the only way to make sure our notebook converter can parse your file!!** 

7. Continue to edit and make changes
7. If you add links to the API or you add images as links (in the assets folder) please do a full build. This will allow you to check if all your
links are correct
   8. `pip install -r requirements.txt`
   9. install node build requires it but you can also comment out in build.sh if you want
      10. https://github.com/nvm-sh/nvm/blob/master/README.md#installing-and-updating
      11. `nvm install node`
   8. If you need the python API `build.sh --skip-ts-api --venv <your venv>`
   9. If you don't need any APIs just images `build.sh --skip-all-api --skip-clone --venv <your venv>`
   10. `cd site/`
   11. `python -m http.server`
5. Don't forget to ask someone to review
6. Reviewnb is set up for this repo but I have not tried it yet. You may need to create an account to see work with the reviews
https://www.reviewnb.com/

Assumptions for the libraries we use in our notebooks:
1. Python 3.11?
2. Fiftyone Latest?
3. Anything else?
