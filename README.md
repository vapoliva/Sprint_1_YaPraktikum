# Sprint_1_YaPraktikum

ЗАДАНИЕ
Это задание — ваш итоговый проект первого спринта. Вы будете сдавать его на проверку через репозиторий на GitHub. А пока сохраните решение в своей IDE.
Верните методу FindTopDocuments возможность быть вызванным со статусом документа вместо лямбды.
Пример
int main() {
    SearchServer search_server;
    search_server.SetStopWords("и в на"s);

    search_server.AddDocument(0, "белый кот и модный ошейник"s,        DocumentStatus::ACTUAL, {8, -3});
    search_server.AddDocument(1, "пушистый кот пушистый хвост"s,       DocumentStatus::ACTUAL, {7, 2, 7});
    search_server.AddDocument(2, "ухоженный пёс выразительные глаза"s, DocumentStatus::ACTUAL, {5, -12, 2, 1});
    search_server.AddDocument(3, "ухоженный скворец евгений"s,         DocumentStatus::BANNED, {9});

    cout << "ACTUAL by default:"s << endl;
    for (const Document& document : search_server.FindTopDocuments("пушистый ухоженный кот"s)) {
        PrintDocument(document);
    }

    cout << "BANNED:"s << endl;
    for (const Document& document : search_server.FindTopDocuments("пушистый ухоженный кот"s, DocumentStatus::BANNED)) {
        PrintDocument(document);
    }

    cout << "Even ids:"s << endl;
    for (const Document& document : search_server.FindTopDocuments("пушистый ухоженный кот"s, [](int document_id, DocumentStatus status, int rating) { return document_id % 2 == 0; })) {
        PrintDocument(document);
    }

    return 0;
} 
Вывод
ACTUAL by default:
{ document_id = 1, relevance = 0.866434, rating = 5 }
{ document_id = 0, relevance = 0.173287, rating = 2 }
{ document_id = 2, relevance = 0.173287, rating = -1 }
BANNED:
{ document_id = 3, relevance = 0.231049, rating = 9 }
Even ids:
{ document_id = 0, relevance = 0.173287, rating = 2 }
{ document_id = 2, relevance = 0.173287, rating = -1 } 
