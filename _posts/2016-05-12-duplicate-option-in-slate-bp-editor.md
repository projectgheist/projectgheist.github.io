---
---

## Feature

Since I use a lot of the same objects in Slate every time, in the same tree, I have to copy and paste the elements every time. I decided that I would add a duplicate Slate element button to the Widget blueprint editor.

## Feature

The first step is to add the button to the mouse menu when right clicking on a tree element. That mouse menu is created in `FWidgetBlueprintEditorUtils::CreateWidgetContextMenu`. We add the duplicate functionality in the `Edit` category during the construction of it.

```
MenuBuilder.BeginSection("Edit", LOCTEXT("Edit", "Edit"));
{
	MenuBuilder.AddMenuEntry(FGenericCommands::Get().Cut);
	MenuBuilder.AddMenuEntry(FGenericCommands::Get().Copy);
	MenuBuilder.AddMenuEntry(FGenericCommands::Get().Paste);
	MenuBuilder.AddMenuEntry(FGenericCommands::Get().Duplicate);
	MenuBuilder.AddMenuEntry(FGenericCommands::Get().Delete);
}
```

The functionality for that new menu item, will now be declared in `FWidgetBlueprintEditor::InitWidgetBlueprintEditor`;

```
DesignerCommandList->MapAction(FGenericCommands::Get().Duplicate,
	FExecuteAction::CreateSP(this, &FWidgetBlueprintEditor::DuplicateSelectedWidgets),
	FCanExecuteAction::CreateSP(this, &FWidgetBlueprintEditor::CanDuplicateSelectedWidgets)
	);
```

... together with callbacks in the same file (don't forget to declare the functions in the header file).

```
bool FWidgetBlueprintEditor::CanDuplicateSelectedWidgets()
{
	TSet<FWidgetReference> Widgets = GetSelectedWidgets();
	return Widgets.Num() > 0;
}

void FWidgetBlueprintEditor::DuplicateSelectedWidgets()
{
	TSet<FWidgetReference> Widgets = GetSelectedWidgets();
	FWidgetBlueprintEditorUtils::CopyWidgets(GetWidgetBlueprintObj(), Widgets);

	FWidgetReference Target = Widgets.Num() > 0 ? *Widgets.CreateIterator() : FWidgetReference();
	
	if (Target.IsValid())
	{
		const UPanelWidget* TargetWidget = CastChecked<UPanelWidget>(Target.GetPreview());
		if (TargetWidget)
		{
			Target = GetReferenceFromPreview(TargetWidget->GetParent());
		}
	}

	FWidgetBlueprintEditorUtils::PasteWidgets(SharedThis(this), GetWidgetBlueprintObj(), Target, PasteDropLocation);
}
```

That's all folks!