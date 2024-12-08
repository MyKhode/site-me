---
title: Game Save System for Unity
published: 2024-12-09
description: 'A reusable static class for implementing Google Play Game save functionality in Unity.'
image: 'https://9to5google.com/wp-content/uploads/sites/4/2016/01/google-play-games-e1453739729404.jpg?quality=82&strip=all&w=1024'
tags: [
    "Unity",
    "Google Play",
    "Game Development"
]
category: 'Code'
draft: false
---

```csharp
using UnityEngine;
using System.Text;
using GooglePlayGames;
using GooglePlayGames.BasicApi;
using GooglePlayGames.BasicApi.SavedGame;

public static class GameSaveUtility
{
    private static bool isLoading = false;
    private static bool isSaving = false;

    
    // Example Usage:
    // Save data
    // SaveData myData = new SaveData { playerName = "John", score = 100 };
    // GameSaveUtility.SaveData("MySaveFile", myData);

    // Load data
    // GameSaveUtility.LoadData<SaveData>("MySaveFile", (data) =>
    // {
    //     Debug.Log($"Player: {data.playerName}, Score: {data.score}");
    // });

    public static void SaveData(string fileName, object data)
    {
        if (!Social.localUser.authenticated)
        {
            Debug.LogError("User is not authenticated to Google Play Services.");
            return;
        }

        if (isSaving)
        {
            Debug.LogError("Already saving data. Please wait...");
            return;
        }

        isSaving = true;

        ((PlayGamesPlatform)Social.Active).SavedGame.OpenWithAutomaticConflictResolution(
            fileName,
            DataSource.ReadCacheOrNetwork,
            ConflictResolutionStrategy.UseMostRecentlySaved,
            (status, metadata) =>
            {
                if (status != SavedGameRequestStatus.Success)
                {
                    Debug.LogError($"Error opening saved game for saving: {status}");
                    isSaving = false;
                    return;
                }

                string jsonString = JsonUtility.ToJson(data);
                byte[] savedData = Encoding.ASCII.GetBytes(jsonString);

                SavedGameMetadataUpdate updatedMetadata = new SavedGameMetadataUpdate.Builder()
                    .WithUpdatedDescription("Save file updated on " + System.DateTime.Now)
                    .Build();

                ((PlayGamesPlatform)Social.Active).SavedGame.CommitUpdate(
                    metadata,
                    updatedMetadata,
                    savedData,
                    (commitStatus, _) =>
                    {
                        if (commitStatus == SavedGameRequestStatus.Success)
                        {
                            Debug.Log("Data saved successfully.");
                        }
                        else
                        {
                            Debug.LogError($"Error saving data: {commitStatus}");
                        }
                        isSaving = false;
                    });
            });
    }

    public static void LoadData<T>(string fileName, System.Action<T> onDataLoaded) where T : class
    {
        if (!Social.localUser.authenticated)
        {
            Debug.LogError("User is not authenticated to Google Play Services.");
            return;
        }

        if (isLoading)
        {
            Debug.LogError("Load already in progress. Please wait...");
            return;
        }

        isLoading = true;

        ((PlayGamesPlatform)Social.Active).SavedGame.OpenWithAutomaticConflictResolution(
            fileName,
            DataSource.ReadCacheOrNetwork,
            ConflictResolutionStrategy.UseLongestPlaytime,
            (status, metadata) =>
            {
                if (status != SavedGameRequestStatus.Success)
                {
                    Debug.LogError($"Error opening saved game for loading: {status}");
                    isLoading = false;
                    return;
                }

                ((PlayGamesPlatform)Social.Active).SavedGame.ReadBinaryData(
                    metadata,
                    (readStatus, savedData) =>
                    {
                        if (readStatus != SavedGameRequestStatus.Success)
                        {
                            Debug.LogError($"Error reading saved game data: {readStatus}");
                            isLoading = false;
                            return;
                        }

                        string jsonString = Encoding.ASCII.GetString(savedData);
                        T data = JsonUtility.FromJson<T>(jsonString);

                        onDataLoaded?.Invoke(data);
                        Debug.Log("Data loaded successfully.");
                        isLoading = false;
                    });
            });
    }
}
```