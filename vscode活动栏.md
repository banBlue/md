在 VSCode 中，可以使用 vscode.window.createTreeView 方法创建一个活动栏，该方法接受两个参数：viewId 和 options。

以下是一个功能丰富的示例代码，该代码创建了一个具有多个子节点和上下文菜单的活动栏：
import * as vscode from 'vscode';

interface Todo {
    label: string;
    description?: string;
    children?: Todo[];
    contextValue?: string;
}

export function activate(context: vscode.ExtensionContext) {
    const todoTreeView = vscode.window.createTreeView('todoList', {
        treeDataProvider: new TodoDataProvider(),
    });

    context.subscriptions.push(
        vscode.commands.registerCommand('todoList.addTodo', (node: Todo | undefined) => {
            const label = node ? `Add child to "${node.label}"` : 'Add Todo';
            vscode.window.showInputBox({ prompt: `Enter label for new todo item:` }).then((value) => {
                if (value) {
                    const todo: Todo = { label: value };
                    if (node) {
                        if (!node.children) {
                            node.children = [];
                        }
                        node.children.push(todo);
                        todoTreeView.refresh(node);
                    } else {
                        todoTreeView
                            .reveal(todo, { expand: 1, select: false, focus: true })
                            .then(() => todoTreeView.refresh());
                    }
                }
            });
        }),

        vscode.commands.registerCommand('todoList.editTodo', (node: Todo) => {
            vscode.window.showInputBox({ prompt: `Enter new label for "${node.label}":`, value: node.label }).then((value) => {
                if (value) {
                    node.label = value;
                    todoTreeView.refresh(node);
                }
            });
        }),

        vscode.commands.registerCommand('todoList.deleteTodo', (node: Todo) => {
            const parentNode = getParentNode(node);
            if (parentNode) {
                const index = parentNode.children?.indexOf(node) ?? -1;
                if (index >= 0) {
                    parentNode.children?.splice(index, 1);
                    todoTreeView.refresh(parentNode);
                }
            } else {
                const index = todoList.indexOf(node);
                if (index >= 0) {
                    todoList.splice(index, 1);
                    todoTreeView.refresh();
                }
            }
        })
    );

    class TodoDataProvider implements vscode.TreeDataProvider<Todo> {
        private _onDidChangeTreeData: vscode.EventEmitter<Todo | null> = new vscode.EventEmitter<Todo | null>();
        readonly onDidChangeTreeData: vscode.Event<Todo | null> = this._onDidChangeTreeData.event;

        getTreeItem(element: Todo): vscode.TreeItem | Thenable<vscode.TreeItem> {
            const treeItem = new vscode.TreeItem(element.label, element.children?.length ? vscode.TreeItemCollapsibleState.Expanded : vscode.TreeItemCollapsibleState.None);
            treeItem.contextValue = element.contextValue;
            treeItem.description = element.description;
            treeItem.command = {
                command: 'todoList.addTodo',
                title: '',
                arguments: [element],
            };
            return treeItem;
        }

        getChildren(element?: Todo): vscode.ProviderResult<Todo[]> {
            if (!element) {
                return todoList;
            } else {
                return