based: [[Uploading Images in mongoose]]

```
import React, { useState } from 'react';

const ImageUploader = () => {
    const [file, setFile] = useState(null);
    const [name, setName] = useState('');
    const [message, setMessage] = useState('');

    const handleFileChange = (event) => {
        setFile(event.target.files[0]); // Set the selected file
    };

    const handleNameChange = (event) => {
        setName(event.target.value); // Set the name typed by user
    };

    const handleSubmit = async (event) => {
        event.preventDefault();
        if (!file) {
            setMessage('Please select a file.');
            return;
        }

        const formData = new FormData();
        formData.append('image', file);
        formData.append('name', name);

        try {
            const response = await fetch('/upload', {
                method: 'POST',
                body: formData,
            });
            if (response.ok) {
                const result = await response.text();
                setMessage(result);
            } else {
                setMessage('Failed to upload image.');
            }
        } catch (error) {
            console.log(error);
            setMessage('An error occurred while uploading.');
        }
    };

    return (
        <div>
            <form onSubmit={handleSubmit}>
                <label>
                    Image Name:
                    <input type="text" value={name} onChange={handleNameChange} />
                </label>
                <label>
                    Upload Image:
                    <input type="file" onChange={handleFileChange} accept="image/*" />
                </label>
                <button type="submit">Upload</button>
            </form>
            {message && <p>{message}</p>}
        </div>
    );
};

export default ImageUploader;

```


## Using react-query

```import React, { useState } from 'react';
import { useMutation } from 'react-query';

const ImageUploader = () => {
    const [file, setFile] = useState(null);
    const [name, setName] = useState('');

    const { mutate, isLoading, isError, error, isSuccess, data } = useMutation(async () => {
        if (!file) {
            throw new Error('No file selected');
        }

        const formData = new FormData();
        formData.append('image', file);
        formData.append('name', name);

        const response = await fetch('/upload', {
            method: 'POST',
            body: formData,
        });

        if (!response.ok) {
            throw new Error('Network response was not ok');
        }
        return response.text();
    });

    const handleFileChange = (event) => setFile(event.target.files[0]);
    const handleNameChange = (event) => setName(event.target.value);

    const handleSubmit = (event) => {
        event.preventDefault();
        mutate(); // Trigger the mutation
    };

    return (
        <div>
            <form onSubmit={handleSubmit}>
                <label>
                    Image Name:
                    <input type="text" value={name} onChange={handleNameChange} />
                </label>
                <label>
                    Upload Image:
                    <input type="file" onChange={handleFileChange} accept="image/*" />
                </label>
                <button type="submit" disabled={isLoading}>Upload</button>
            </form>
            {isSuccess && <p>{data}</p>}
            {isError && <p>Error: {error.message}</p>}
        </div>
    );
};

export default ImageUploader;

```