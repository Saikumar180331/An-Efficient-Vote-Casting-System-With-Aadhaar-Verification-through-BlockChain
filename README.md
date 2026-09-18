# An Efficient Vote Casting System with Aadhar Verification through Blockchain

A secure, transparent, and tamper-proof electronic voting system built with **Django**, **Ethereum Smart Contracts (Solidity)**, and **Biometric Fingerprint Matching (OpenCV + Scikit-Image)**.

---

## 📌 Table of Contents
- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Project Directory Structure](#-project-directory-structure)
- [Prerequisites & Installation](#-prerequisites--installation)
- [How to Run the Application](#-how-to-run-the-application)
- [Step-by-Step User Guide](#-step-by-step-user-guide)
  - [Admin Workflow](#1-admin-workflow)
  - [Voter Workflow](#2-voter-workflow)
- [Biometric Fingerprint Matching Algorithm](#-biometric-fingerprint-matching-algorithm)
- [Blockchain & Smart Contract Integration](#-blockchain--smart-contract-integration)

---

## 📖 Overview

Traditional voting systems face vulnerabilities such as bogus voting, identity impersonation, and database tampering. Electronic Voting Machines (EVMs) connected to centralized databases can be vulnerable to network attacks or data manipulation.

This project addresses these challenges by combining **Blockchain technology** with **Aadhar-linked Biometric Fingerprint Verification**:
1. **Biometric Authentication**: Prevents duplicate or fraudulent voting by verifying voter fingerprint minutiae against stored Aadhar biometric records using OpenCV & Scikit-Image feature extraction.
2. **Ethereum Blockchain**: Stores candidate details, voter registrations, and cast votes on an immutable, encrypted decentralized ledger using Solidity smart contracts (`Voting.sol`).
3. **Transparent Auditing**: Allows instant tallying of election results and transaction latency graph visualization.

---

## ✨ Key Features

### 🛡️ Admin Module
- **Admin Authentication**: Secure login interface (`admin` / `admin`).
- **Candidate Registration**: Register candidates with name, party affiliation, contest area, and party symbol image.
- **Voter Registration**: Register voters with contact details, Aadhar number, and biometric fingerprint image (`.tif`).
- **Add Election Date**: Set and publish official election dates. Voting is restricted exclusively to scheduled dates.
- **View Vote Count**: Real-time tallying of votes cast per candidate.

### 🗳️ Voter / User Module
- **Voter Authentication**: Login via Username, Password, and Uploaded Fingerprint image.
- **Aadhar Biometric Verification**: Automatically matches uploaded fingerprint against registered Aadhar fingerprint database using CLAHE, ORB descriptors, skeletonization, and brute-force matcher (`BFMatcher`).
- **Cast Vote**: Select candidate and cast vote securely on the blockchain.
- **Double-Voting Prevention**: Ensures each registered voter can cast only one vote per election.
- **Blockchain Latency Graph**: Plot real-time transaction latency vs. transaction numbers using Matplotlib.
- **View Election Results**: Publicly view election outcomes and total vote counts.

---

## 🏗️ System Architecture

```
+-----------------------------------------------------------------------+
|                            USER INTERFACE                             |
|       (Admin Dashboard / Voter Dashboard - HTML5, CSS3, JS)           |
+-----------------------------------+-----------------------------------+
                                    |
                                    v
+-----------------------------------+-----------------------------------+
|                        DJANGO WEB FRAMEWORK                           |
|      (Routing, Views, Session Management, Static File Storage)        |
+-----------------+---------------------------------+-------------------+
                  |                                 |
                  v                                 v
+-----------------+-----------------+     +---------+-----------------+
|   FINGERPRINT MATCHING ENGINE     |     |   BLOCKCHAIN LAYER        |
|  (OpenCV, Skimage, ORB Descriptors|     |  (Web3.py + Ethereum RPC  |
|  Skeletonization & Harris Corners)|     |  Solidity Voting.sol)     |
+-----------------------------------+     +---------------------------+
```

---

## 🛠️ Technology Stack

- **Backend Framework**: Python 3.7 / Django 2.1.7
- **Blockchain Layer**: Solidity, Ethereum Web3 (v4.7.2), JSON ABI Contract Provider (with built-in RPC fallback)
- **Computer Vision & Image Processing**: OpenCV (`opencv-python` 4.1, `opencv-contrib-python`), `scikit-image`, `numpy`, `scipy`
- **Visualization**: `matplotlib` (Base64 graph plotting)
- **Frontend**: HTML5, Vanilla CSS3 (`default.css`), JavaScript
- **Database**: SQLite3 (for local media storage) & Ethereum Ledger (for core voting records)

---

## 📁 Project Directory Structure

```
AadharVoting/
├── Voting/                         # Django Project Settings
│   ├── settings.py                 # Core configurations & ALLOWED_HOSTS
│   ├── urls.py                     # Primary routing table
│   └── wsgi.py                     # WSGI gateway interface
├── VotingApp/                      # Main Django Application
│   ├── templates/                  # HTML UI Views
│   │   ├── index.html              # Home Page
│   │   ├── Admin.html              # Admin Login
│   │   ├── AdminScreen.html        # Admin Dashboard
│   │   ├── AddCandidate.html       # Candidate Registration Form
│   │   ├── AddVoter.html           # Voter Registration Form
│   │   ├── AddElectionDate.html    # Set Election Date
│   │   ├── User.html               # Voter Login with Fingerprint
│   │   ├── UserScreen.html         # Voter Dashboard & Graph
│   │   ├── Vote.html               # Candidate Selection & Voting Table
│   │   └── ViewResult.html         # Vote Tally Screen
│   ├── static/                     # CSS, Party Symbols & Fingerprint Images
│   ├── views.py                    # Application Business Logic & Web3 Callbacks
│   └── urls.py                     # App Route Handlers
├── FingerMatch.py                  # Biometric Fingerprint Minutiae Matching Algorithm
├── enhance/                        # Image Enhancement Module (Gabor Filters & Thinning)
├── SampleFingers/                  # Sample Fingerprint Datasets (.tif format)
├── Voting.sol                      # Solidity Smart Contract Source
├── Voting.json                     # Compiled Contract ABI & Artifacts
├── db.sqlite3                      # Local SQLite Database
├── manage.py                       # Django CLI Utility
├── requirements.txt                # Python Dependencies List
└── README.md                       # Project Documentation
```

---

## ⚙️ Prerequisites & Installation

### 1. Requirements
Ensure **Python 3.7+** is installed on your system.

### 2. Clone / Extract Repository
Navigate to the project root directory:
```bash
cd AadharVoting/AadharVoting
```

### 3. Install Python Dependencies
Install required packages using pip:
```bash
pip install numpy==1.21.6 pandas==1.3.5 matplotlib==3.1.1 Django==2.1.7 requests==2.28.1 web3==4.7.2 scipy==1.7.3 opencv-python==4.1.1.26 opencv-contrib-python==4.3.0.36 scikit-image
```
*Or directly install from `requirements.txt`:*
```bash
pip install -r requirements.txt
```

---

## 🚀 How to Run the Application

### Start Development Server
Run the Django server on port `8000`:
```bash
python manage.py runserver 0.0.0.0:8000
```

Open your browser and navigate to:
```
http://127.0.0.1:8000/
```

*(Optional: To run on local Ethereum node, start Ganache or Truffle local node on `http://127.0.0.1:9545`. The app automatically falls back to an in-memory blockchain mock if Ganache is offline).*

---

## 📝 Step-by-Step User Guide

### 1. Admin Workflow

1. Click **Admin Login** from the Home Page.
2. Login with credentials:
   - **Username**: `admin`
   - **Password**: `admin`
3. **Register Candidates**:
   - Click `Candidate Registration`.
   - Fill in Candidate Name, Party Name, Area, Aadhar Number, and upload Party Symbol image (`.jpg`/`.png`).
   - Click **Submit** to store candidate on the Blockchain.
4. **Register Voters**:
   - Click `Voter Registration`.
   - Enter Voter Username, Password, Contact, Email, Address, Aadhar Number.
   - Upload fingerprint image (e.g. choose sample file `SampleFingers/1.tif`).
   - Click **Submit** to register voter details on Blockchain and store biometric template.
5. **Set Election Date**:
   - Click `Add Election Date`.
   - Enter today's date in `YYYY-MM-DD` format (e.g., `2026-09-18`) so voting is active.

### 2. Voter Workflow

1. Click **User Login** from the Home Page.
2. Enter registered **Username**, **Password**, and upload matching **Fingerprint Image** (e.g. `SampleFingers/1.tif`).
3. Click **Login**:
   - The system enhances fingerprint image using Gabor filters, extracts ORB keypoints, skeletonizes ridges, and computes minutiae distance against registered Aadhar fingerprints.
   - Upon successful verification, you are redirected to the **Voter Dashboard**.
4. **Cast Vote**:
   - Click `Cast Your Vote`.
   - Review list of candidates and click **Click Here** next to your preferred candidate.
   - The vote transaction is signed and committed to the Blockchain ledger.
   - Attempting to vote a second time will display: *"You already casted vote"*.
5. **View Results & Latency Graph**:
   - Click `View Result` to check updated candidate vote counts.
   - Click `Latency Graph` to inspect real-time Blockchain execution latency plots.

---

## 🔍 Biometric Fingerprint Matching Algorithm

The matching pipeline in [`FingerMatch.py`](file:///c:/Users/mucha/OneDrive/Desktop/8688/1/AadharVoting/AadharVoting/FingerMatch.py) works through 5 stages:
1. **Histogram Equalization**: Contrast enhancement using CLAHE (`cv2.createCLAHE`).
2. **Gabor Filter Enhancement**: Ridge orientation & frequency enhancement (`enhance/image_enhance.py`).
3. **Thresholding & Skeletonization**: Otsu binarization and morphological skeletonization (`skimage.morphology.skeletonize`).
4. **Spurious Dot Removal & Minutiae Extraction**: Removes isolated artifacts and detects minutiae via Harris Corner Detection (`cv2.cornerHarris`).
5. **Descriptor Matching**: Extract ORB descriptors (`cv2.ORB_create`) and perform Hamming distance matching with `cv2.BFMatcher`. Matches with mean distance score below threshold (< 10) confirm identity.

---

## ⛓️ Blockchain & Smart Contract Integration

The Solidity smart contract [`Voting.sol`](file:///c:/Users/mucha/OneDrive/Desktop/8688/1/AadharVoting/AadharVoting/Voting.sol) maintains ledger state for voters, candidates, and votes:

```solidity
contract Voting {
    struct User { string username; string email; string password; string contact; string home_address; string aadhar; }
    struct Party { string candidate_name; string party_name; string area; string party_symbol; string aadhar; }
    struct Vote { string user; string party; string date_str; string candidate; }

    function createUser(...) public;
    function createParty(...) public;
    function createVote(...) public;
    function getUserCount() public view returns(uint);
    function getPartyCount() public view returns(uint);
    function getVotingCount() public view returns(uint);
}
```

The Web3 integration layer in [`views.py`](file:///c:/Users/mucha/OneDrive/Desktop/8688/1/AadharVoting/AadharVoting/VotingApp/views.py) automatically handles transaction generation and receipt validation.