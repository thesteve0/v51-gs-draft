# Quickstart

## Intro
Welcome to the quickstart for FiftyOne. This lesson is the simplest possible introduction to FiftyOne and only aims to have you see the 2 major parts of the platform, the SDK and the App. It's best if you consider this as a "smoketest" to make sure you have everything installed correctly and working on your machine. Once you complete this, if you are new to FiftyOne then you should go to the more in-depth [Beginners Getting TODO](theguide.ipynb) Started guide. If you are familiar with some areas of FiftyOne then it might be more appropriate for you to go to one of the more [focused Getting TODO](rootof/the/listsings.md?) Started guides

### Who this is for

This lesson assumes zero familiarity with FiftyOne or even computer vision. We do assume you have a basic understanding of Python and the use of its virtual environments.

We assume you want to install Fiftyone, make sure it works, and see how to access the main parts of the platform.

### Time to complete

Doing this lesson, beyond download and installation, should take about 5 minutes

### Content
There will be 3 sections to this document

1. Installation
2. Using the SDK
3. Opening the App


## Installation

The installation instructions here are not complete and do not cover some of the caveats. For a more thorough discussion of installing fiftyone please consult the [install documentation](../../../fiftyone_concepts/install.md). We assume you have Python versions between 3.9 and 3.12. To check your Python version, at the command prompt, run:

```shell
python --version
```
To avoid conflicts with other Python packages installed on your system and for overall best practice, we are going to create a [virtual environment](https://docs.python.org/3/library/venv.html). A virtual environment creates a sandbox with the Python executable and all the installed packages will be stored. The directory is typically named "venv" or ".venv" and created in the projects directory. The names and locations are flexible but we will use standard conventions here. You can read more in our [virtual environment](../../../fiftyone_concepts/virtualenv.md) documentation.

In your project directory, run the following command to create a virtual environment named ".venv".

```shell
python -m venv .venv
```

Now we need to activate the virtual environment. Activating the virtual environment ensures that all the Python commands run in the current terminal use the Python in our virtual environment, all Python libraries will be installed in it, and they will be the only libraries visible to our Python applications we run.

On Linux, Mac, and WSL:

```shell
source ./.venv/bin/activate
```

On Windows:

```shell
.venv\Scripts\activate
```

With best practices in place, now we can install Fiftyone. In the command prompt enter:

```shell
pip install fiftyone
```

You should see lines start scrolling by as the installer gathers requirements for the installation. When the command is finished running you should see something similar to this in the terminal:

```shell
Successfully installed Deprecated-1.2.18 Jinja2-3.1.6 MarkupSafe-3.0.2 Pillow-11.1.0 PyYAML-6.0.2 aiofiles-24.1.0 anyio-4.9.0 argcomplete-3.6.1 attrs-25.3.0 beautifulsoup4-4.13.3 boto3-1.37.23 botocore-1.37.23 brotli-1.1.0 cachetools-5.5.2 certifi-2025.1.31 charset-normalizer-3.4.1 contourpy-1.3.1 cycler-0.12.1
    ...
    tifffile-2025.3.13 typing-extensions-4.13.0 tzdata-2025.2 tzlocal-5.3.1 universal-analytics-python3-1.1.1 urllib3-2.3.0 voxel51-eta-0.14.0 wcwidth-0.2.13 wrapt-1.17.2 wsproto-1.2.0 xmltodict-0.14.2
```

and then your command prompt waiting for input. If this is not what you see then our [troubleshooting guide](../../../fiftyone_concepts/troubleshooting.md) should help you understand how to correct the problems.

With that you have successfully installed FiftyOne

## Using the SDK

The SDK provides a Python library that allows you to load your data into FiftyOne and then use Python to query, manipulate, and understand your visual data. You can also then visualize that data by opening the App via the SDK pointing at your data. We will discuss the app in the next section.

To understand more of the SDK you can look at the [FiftyOne Concepts](../../../fiftyone_concepts/) section of our documentation which goes more in depth on all the various features and functionality of the SDK.

From outside of a Notebook, you can start up Python in your favorite manner, either at the [REPL](https://docs.python.org/3/tutorial/interpreter.html) or start a file in your favorite IDE. Please note, if you are going to use an IDE, make sure that the IDE is using the virtual environment we created in the previous section. Here are instructions for the [Jetbrains family](https://www.jetbrains.com/help/pycharm/configuring-python-interpreter.html#add-existing-interpreter) of IDEs, such as PyCharm or IDEA, and here are the instructions for [Visual Studio code](https://code.visualstudio.com/docs/python/environments#_working-with-python-interpreters). For the rest of the instructions we are going to use the [Jupyter notebook](https://jupyter.org/) environment.

Time for code!






```python
# Import the fiftyone main library and the zoo library
# The zoo contains datasets and computer vision models already converted to FiftyOne format
import fiftyone as fo
import fiftyone.zoo as foz
```

## Datasets

Now that we have loaded the library let's grab a dataset from the [FiftyOne Data Zoo](https://docs.voxel51.com/data/dataset_zoo). We set `persistent = True` so that any changes we make to the [dataset are retained](../../../fiftyone_concepts/using_datasets/#dataset-persistence) and available the next time we start FiftyOne.


```python
dataset = foz.load_zoo_dataset("quickstart", persistent=True)
fo.list_datasets()
```

    Dataset already downloaded
    Loading existing dataset 'quickstart'. To reload from disk, either delete the existing dataset or provide a custom `dataset_name` to use





    ['fashion-mnist', 'photo-album', 'ppe', 'ppe-test', 'ppe-train', 'quickstart']



A [Dataset](../../../api/fiftyone.core.dataset.Dataset.html) is one of the fundamental objects in the FiftyOne API. It represents the collection of media files you are going to work with. Any work you do will first require you to have a Dataset object. We are only briefly discussing Datasets here, it is well worth your time to read the [Basics](https://beta-docs.voxel51.com/fiftyone_concepts/basics/) and [Using Datasets](https://beta-docs.voxel51.com/fiftyone_concepts/using_datasets/) sections of the FiftyOne Concepts documentation.

Note: your media files are not stored in the dataset, they remain in place on disk. The Dataset is composed of samples with one sample per media item. We will explain samples later. Each sample has a field which points to the location of the file. You can not directly edit the media file from within FiftyOne but, you can use the reference field of the sample to pass the file location to your code that does alter the image.

Let's look at some information about our Dataset. There are three different ways to get information about the Dataset, two which are almost identical


```python
print("Just the dataset")
print(dataset)

print("\ndataset.schema")
print(dataset.schema)

print("\ndataset.stats()")
dataset.stats(include_media=True, compressed=True)


```

    Just the dataset
    Name:        quickstart
    Media type:  image
    Num samples: 200
    Persistent:  True
    Tags:        []
    Sample fields:
        id:               fiftyone.core.fields.ObjectIdField
        filepath:         fiftyone.core.fields.StringField
        tags:             fiftyone.core.fields.ListField(fiftyone.core.fields.StringField)
        metadata:         fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.metadata.ImageMetadata)
        created_at:       fiftyone.core.fields.DateTimeField
        last_modified_at: fiftyone.core.fields.DateTimeField
        ground_truth:     fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.labels.Detections)
        uniqueness:       fiftyone.core.fields.FloatField
        predictions:      fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.labels.Detections)
    
    dataset.schema
    <bound method SampleCollection.schema of Name:        quickstart
    Media type:  image
    Num samples: 200
    Persistent:  True
    Tags:        []
    Sample fields:
        id:               fiftyone.core.fields.ObjectIdField
        filepath:         fiftyone.core.fields.StringField
        tags:             fiftyone.core.fields.ListField(fiftyone.core.fields.StringField)
        metadata:         fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.metadata.ImageMetadata)
        created_at:       fiftyone.core.fields.DateTimeField
        last_modified_at: fiftyone.core.fields.DateTimeField
        ground_truth:     fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.labels.Detections)
        uniqueness:       fiftyone.core.fields.FloatField
        predictions:      fiftyone.core.fields.EmbeddedDocumentField(fiftyone.core.labels.Detections)>
    
    dataset.stats()





    {'samples_count': 200,
     'samples_bytes': 913408,
     'samples_size': '892.0KB',
     'media_bytes': 24412374,
     'media_size': '23.3MB',
     'total_bytes': 25325782,
     'total_size': '24.2MB'}



We'll start by explaining the output from `output.stats()`, which is primarily concerned with storage size. From this output we can see the number of samples in the dataset, the total size of the collection of sample records in the dataset, the total size of the actual media files referenced in the samples, and then the total size both pieces combined.

Outputting dataset with `print(dataset)` returns the string representation of the dataset, while calling `dataset.schema` returns the same information bound in a Schema object. Other than that, the information they return is the same. You can see how many samples are in the dataset, other high level metadata about the dataset like tags, and then the name and types of the fields found on all samples.  Which is a good segue to samples and fields.

### Samples



### Fields


```python

```

## Using the App

Let's go ahead and open the App so we can visualize our data. We launch the app, point it at our dataset and set `auto=False` to prevent the visual component of the application being launched inside a notebook output cell. The `session` object returned is a handle to the app server running in the background. The server is a singleton so as long as it is running any new calls that create a session will actually return a handle to the same server.

We then tell the session to open a tab outside the Jupyter notebook - this is a much better way to interact with the application.

Note: By default as soon as the Python process that launched the app exits the server will shutdown. This mean, if you are running code outside a REPL or a notebook the server will close when you code exits. If you are running code then you are going to want to tell the session to block the main thread to prevent the code from finishing. You can do this by adding `session.wait()` after you launch the app. As the [API doc](https://beta-docs.voxel51.com/api/fiftyone.core.session.session.Session.html#wait) says, "All connected windows must be closed before this method unblocks. "


```python
session = fo.launch_app(dataset, auto=False)
session.open_tab()
```

    Session launched. Run `session.show()` to open the App in a cell output.



    <IPython.core.display.Javascript object>



```python
session.selected
```




    ['67edd4b96730c3f9d3960f57']


