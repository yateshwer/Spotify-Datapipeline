# Spotify ETL Project

This project is an ETL (Extract, Transform, Load) pipeline designed to fetch data from a Spotify playlist, transform it into usable formats, and store it in an AWS S3 bucket. The pipeline leverages the Spotify API and AWS Lambda, and it’s designed to be serverless.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Architecture](#architecture)
- [Setup Instructions](#setup-instructions)
- [Functions](#functions)
- [Folder Structure](#folder-structure)
- [License](#license)

---

## Project Overview

This ETL pipeline:
1. **Extracts** data from a specified Spotify playlist using the Spotify API.
2. **Transforms** the data by breaking it down into three tables: albums, artists, and songs.
3. **Loads** the transformed data as CSV files into specified folders within an S3 bucket. 

This project could be useful for analytics projects, playlist research, or data science applications that require structured Spotify data.

---

## Features

- **Serverless Execution**: Deployed on AWS Lambda, making the ETL process scalable and cost-effective.
- **Data Storage in S3**: Stores raw and processed data in Amazon S3 for secure, centralized access.
- **Data Transformation**: Extracts relevant fields and organizes them into CSV files for easy querying.
- **Automated Data Movement**: Moves processed files from the `to_processed` folder to the `processed` folder.

---

## Architecture

1. **Spotify API**: Fetches playlist data.
2. **AWS Lambda**: Executes ETL functions automatically.
3. **AWS S3**: Stores raw JSON files and transformed CSV files.

---

## Setup Instructions

### Prerequisites
- **AWS Account** with permissions to create Lambda functions and S3 buckets.
- **Spotify Developer Account** for API access.
  - Register an application and get a `client_id` and `client_secret`.
- **Python 3.x** with `boto3` and `spotipy` libraries installed.

### Environment Variables

Set the following environment variables in your AWS Lambda function:
- `client_id`: Spotify API Client ID
- `client_secret`: Spotify API Client Secret

### Deployment

1. **Create an S3 Bucket**: Create a bucket to store raw and transformed data. Update the bucket name in the code if needed.
2. **Upload the Code**: Deploy the provided Python code to your AWS Lambda function.
3. **Set Triggers**: Configure AWS Lambda to run the function as needed (e.g., scheduled or event-based).

---

## Functions

### 1. Extract Spotify Data
- Uses `Spotipy` to fetch playlist data from Spotify.
- Saves the data in raw JSON format in the S3 bucket under `raw_data/to_processed/`.

### 2. Data Transformation
- **Albums**: Extracts `album_id`, `name`, `release_date`, `total_tracks`, and `url`.
- **Artists**: Extracts `artist_id`, `artist_name`, and `external_url`.
- **Songs**: Extracts `song_id`, `song_name`, `duration_ms`, `url`, `popularity`, `song_added`, `album_id`, and `artist_id`.
- Saves each entity as a separate CSV in the S3 bucket under `transformed_data`.

### 3. Move and Delete Raw Data
- After processing, moves JSON files to `raw_data/processed/` and deletes them from `raw_data/to_processed/`.

---

## Folder Structure

The S3 bucket has the following structure:

