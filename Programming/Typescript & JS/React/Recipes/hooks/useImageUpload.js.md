based on: [[Uploading Images in mongoose]]

```
// hooks/useImageUpload.js
import { useMutation } from 'react-query';

const useImageUpload = () => {
    return useMutation(async ({ file, name }) => {
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
};

export default useImageUpload;

```


### Usage:

```
// components/ImageUploader.js
import React, { useState } from 'react';
import useImageUpload from '../hooks/useImageUpload'; // Adjust path as necessary

const ImageUploader = () => {
    const [file, setFile] = useState(null);
    const [name, setName] = useState('');
    const { mutate, isLoading, isError, error, isSuccess, data } = useImageUpload();

    const handleFileChange = (event) => setFile(event.target.files[0]);
    const handleNameChange = (event) => setName(event.target.value);

    const handleSubmit = (event) => {
        event.preventDefault();
        mutate({ file, name }); // Pass file and name to the mutation
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