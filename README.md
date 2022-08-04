# pdf-diff
A tool for visualizing differences between two pdf files. Mainly dedicated to editors that spent a lot of hours on several pdf.

![Example of output](https://raw.githubusercontent.com/serhack/pdf-diff/main/image-1.png)

## Foreword

I use [Indesign](https://www.adobe.com/it/products/indesign.html) almost daily, and the pagination and convenient graphical interface make that product number 1 among desktop publishing programs. Indesign, as well as many other graphics programs, have one flaw: because they are not based on any versioning tool, it is difficult to compare two versions of the same file

I sometimes have to do some retouching to files I produce. Be they resumes, books or technical manuals. However, if editing a resume is very easy, editing large volumes is much more difficult. Several times, sharing the result of pdfs with my team, we could not clearly visualize the differences between one version and another. This is compounded by human error: with more than 50-60 pages to review, it is impossible to keep track of all the changes between versions! 

Therefore, I developed through the powerful go programming language a new tool called `pdf-diff`. Pdf-diff allows you to create images that show exactly where the pdf has changed, thus displaying the changes from one version to another. 

## How it works

From a technical point of view, the tool is very simple and trivial. Pdf-diff uses pdftoppm to generate a series of images from the pdfs to be compared (one for each page). It then uses a very trivial pixel comparison algorithm to draw some red rectangles that display the differences between one pdf and another. The difference is based on RGB values of the pixel, so it can basically compare whatever you want. The go script also uses golang's very powerful native encoding/decoding image engine (which I personally was not familiar with!). I was very impressed with what is possible to do with Go in just a few lines of code.

The images generated by pdf are inserted into a folder named as the hash of the content of the pdf file. E.g. the file has the hash `fc324..`, the images are in the `fc324` folder. If a folder with that name already exists, pdf-diff will not create any images since it consider that images were already generated.

The code is not very clean and certainly can be optimized. I am asking some person much more knowledgeable than me in graphics if it is possible to create a simple algorithm that can apply a background color only locally, and not on the whole row where the pixel is changed.

## How to use

The only requirement asked for running this tool is the `pdftoppm` program. Based on your operating system or distro, you might want to check `poppler-utils` package. A command for installing that tool in Ubuntu/Debian distro might be:

```
apt install poppler-utils
```

To run the script, you can simply open a new shell and type:

```
go run main.go ./pdf-1.pdf ./pdf-2.pdf
```

or:

```
go build
./main pdf-1.pdf pdf-2.pdf
```

Once ran, the images are created in the folder `generated`.

### Contact

If you wish to use this for your project, go ahead. If you have any issues or improvements, feel free to open a new [ISSUE]. Lastly, if you have a good algorithm to implement or just to discuss about any other tools for editor, you can [email me](hi@serhack.me).

#### Donation

If you think my work contributed a little bit to your projects, goals or company, please let me know.

Monero: `47VFueCo1yvc6nq688QsBt9UZSrg5z2JLFUwWFs4WtHBSwDsybDbnmLiydo46ybPeqSMxypnjmz5pdz87t4VjngfQfmMd4S`
Bitcoin: `1Pt3YwkFoexAA3s9pV3saoJ2EAXzpqBmrp`