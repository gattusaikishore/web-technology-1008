<!DOCTYPE html>
<html lang="en" ng-app="libraryApp">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Library Management</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.8.2/angular.min.js"></script>
    <style>
        table {
            width: 50%;
            border-collapse: collapse;
            margin: 20px auto;
        }
        table, th, td {
            border: 1px solid black;
            text-align: center;
            padding: 8px;
        }
        th {
            background-color: #f4f4f4;
        }
        form {
            width: 50%;
            margin: 20px auto;
            text-align: center;
        }
        input, button {
            margin: 5px;
        }
    </style>
</head>
<body ng-controller="LibraryController">

    <h1 style="text-align: center;">Library Management</h1>

    <table>
        <thead>
            <tr>
                <th>Category</th>
                <th>Book Count</th>
            </tr>
        </thead>
        <tbody>
            <tr ng-repeat="item in library">
                <td>{{ item.category }}</td>
                <td><input type="number" ng-model="item.count" /></td>
            </tr>
        </tbody>
    </table>

    <form ng-submit="addCategory()">
        <input type="text" ng-model="newCategory.name" placeholder="Category Name" required />
        <input type="number" ng-model="newCategory.count" placeholder="Initial Book Count" required />
        <button type="submit">Add Category</button>
        <p style="color: red;" ng-if="errorMessage">{{ errorMessage }}</p>
    </form>

    <script>
        angular.module('libraryApp', [])
        .controller('LibraryController', ['$scope', function($scope) {
            $scope.library = [
                { category: 'Fiction', count: 120 },
                { category: 'Non-Fiction', count: 80 },
                { category: 'Science', count: 150 },
                { category: 'Mathematics', count: 70 }
            ];
            $scope.newCategory = { name: '', count: null };
            $scope.errorMessage = '';
            $scope.addCategory = function() {
                const existingCategory = $scope.library.find(item => item.category.toLowerCase() === $scope.newCategory.name.toLowerCase());
                if (existingCategory) {
                    $scope.errorMessage = 'Category name must be unique!';
                } else {
                    $scope.library.push({ category: $scope.newCategory.name, count: $scope.newCategory.count });
                    $scope.newCategory = { name: '', count: null };
                    $scope.errorMessage = '';
                }
            };
        }]);
    </script>
</body>
</html>
